---
aliases: 
tags: 
date created: terça-feira, novembro 26º 2024, 2:29:35 pm
date modified: terça-feira, novembro 26º 2024, 4:26:28 pm
---
É possível identificar o tenant id pela rota e conferir no HTTPCONTEXT se de fato aquele usuário tem permissão para acessar dados daquele tenant.

Exemplo:
 
```cs
public class TenantData : ITenantData
{
    private readonly IHttpContextAccessor _httpContextAccessor;

    public TenantData(IHttpContextAccessor httpContextAccessor)
    {
        _httpContextAccessor = httpContextAccessor;
    }

    public string GetTenantId()
    {
        return _httpContextAccessor.HttpContext.GetTenantId();
    }
}

public static class HttpContextExtensions
{
    public static string GetTenantId(this HttpContext httpContext)
    {
        return httpContext.GetRouteValue("tenantId");
    }
}

public class ApplicationContext : DbContext
{
    private readonly ITenantData _tenantData;

    public override string TenantId => _tenantData.GetTenantId();

	public override OnSaveChanges()
  {
    // Verificar se o usuário tem permissão para acessar o tenant

	var modelsChanged = ChangeTracker.Entries().Where(x => x.State == EntityState.Added || x.State == EntityState.Modified || x.State == EntityState.Deleted).ToList();

	foreach (var model in modelsChanged)
	{
	  if (model.Entity is ITenantEntity tenantEntity)
    {
      if (tenantEntity.TenantId != TenantId)
      {
        throw new Exception("Usuário não tem permissão para acessar este tenant");
      }
    }
  }
}

```

---

1 - The base class:

```cs
public class BaseEntity
{
    public int TenantId { get; set; }
}

public class Product : BaseEntity
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```

The filter by scope using HTTPContextAcessor:

```cs
public interface ITenantProvider
{
    int TenantId { get; }
}

public class TenantProvider : ITenantProvider
{
    private readonly IHttpContextAccessor _httpContextAccessor;

    public TenantProvider(IHttpContextAccessor httpContextAccessor)
    {
        _httpContextAccessor = httpContextAccessor;
    }

    public int TenantId
    {
        get
        {
            // Example: Extract TenantId from headers or claims
            return int.Parse(_httpContextAccessor.HttpContext?.User?.FindFirst("TenantId")?.Value ?? "0");
        }
    }
}
```

Program.cs:

```cs
services.AddHttpContextAccessor();
services.AddScoped<ITenantProvider, TenantProvider>();
```

AppDbContext:

```cs
public class ApplicationDbContext : DbContext
{
    private readonly ITenantProvider _tenantProvider;

    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options, ITenantProvider tenantProvider)
        : base(options)
    {
        _tenantProvider = tenantProvider;
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        // Apply global query filter for entities with TenantId
        foreach (var entityType in modelBuilder.Model.GetEntityTypes())
        {
            if (typeof(BaseEntity).IsAssignableFrom(entityType.ClrType))
            {
                var parameter = Expression.Parameter(entityType.ClrType, "e");
                var tenantProperty = Expression.Property(parameter, nameof(BaseEntity.TenantId));
                var currentTenant = Expression.Constant(_tenantProvider.TenantId);
                var filterExpression = Expression.Lambda(
                    Expression.Equal(tenantProperty, currentTenant), parameter);

                modelBuilder.Entity(entityType.ClrType).HasQueryFilter(filterExpression);
            }
        }
    }

    public DbSet<Product> Products { get; set; }

	public override int SaveChanges()
	{
	    SetTenantId();
	    return base.SaveChanges();
	}
	
	public override async Task<int> SaveChangesAsync(CancellationToken cancellationToken = default)
	{
	    SetTenantId();
	    return await base.SaveChangesAsync(cancellationToken);
	}
	
	private void SetTenantId()
	{
	    foreach (var entry in ChangeTracker.Entries<BaseEntity>())
	    {
	        if (entry.State == EntityState.Added)
	        {
	            entry.Entity.TenantId = _tenantProvider.TenantId;
	        }
	    }
	}

}
```

