# 🔁 Repository Design Pattern vs Generic Repository

## 📋 Karşılaştırmalı Tablo

| Özellik | Repository Design Pattern | Generic Repository |
|--------|----------------------------|--------------------|
| 🎯 **Tanım** | Her entity (varlık) için ayrı repository yazılır | Tüm entity'ler için ortak tek bir repository yazılır |
| 🔧 **Yapı** | `IProductRepository`, `ICustomerRepository` gibi sınıflar ayrı ayrı tanımlanır | `IGenericRepository<T>` şeklinde generic interface kullanılır |
| 🧠 **Kod Tekrarı** | Yüksektir, her entity için CRUD işlemleri ayrı yazılır | Düşüktür, tüm CRUD işlemleri tek sınıfta tanımlanır |
| 🔍 **Özelleştirme Kolaylığı** | Her entity’ye özel sorgular/metotlar yazmak kolaydır | Özelleştirme için generic sınıfın override edilmesi gerekir |
| 🛠 **Kullanım Kolaylığı** | Karmaşık ama güçlü kontrol sağlar | Pratik ve sade yapı sunar (CRUD için idealdir) |
| 💡 **Tipik Kullanım** | Karmaşık domain modellerinde özel query'ler gerektiğinde | Küçük/orta ölçekli, CRUD tabanlı projelerde |
| 🧪 **Test Edilebilirlik** | Yüksek | Yüksek (özellikle mock repository ile) |
| ⚖️ **Esneklik** | Çok esnek yapı sunar | Orta düzeyde esnek, ihtiyaç halinde genişletilir |

---

## 📌 Özetle

| Soru | Cevap |
|------|-------|
| **Generic Repository ne sağlar?** | Kod tekrarını azaltır, tüm entity’ler için tek bir yapı sunar. |
| **Repository Pattern ne sağlar?** | Her entity için özel ve özelleştirilebilir yapı sunar. |
| **Hangisi daha güçlüdür?** | Repository Pattern özelleştirme açısından daha güçlüdür. |
| **Hangisi daha pratiktir?** | Generic Repository kod sadeleştirmede daha pratiktir. |

---

## 🎯 Ne Zaman Hangisini Kullanmalı?

- ✔️ Projen büyük, her entity için özel işlemler gerektiriyorsa → **Repository Design Pattern**
- ✔️ Sade CRUD işlemleri varsa, kod tekrarını önlemek istiyorsan → **Generic Repository**
- ✔️ En iyi çözüm: **Hibrit kullanım**  
  - Ortak işlemler için: `GenericRepository<T>`  
  - Özel işlemler için: `ProductRepository : GenericRepository<Product>`


## 📦 Ortak Senaryo: `Product` Entity
```csharp
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```

---

## ✅ KLASİK REPOSITORY DESIGN PATTERN

### 1. Interface
```csharp
public interface IProductRepository
{
    Product GetById(int id);
    IEnumerable<Product> GetAll();
    void Add(Product product);
    void Update(Product product);
    void Delete(int id);
}
```

### 2. Concrete Repository
```csharp
public class ProductRepository : IProductRepository
{
    private readonly DbContext _context;

    public ProductRepository(DbContext context)
    {
        _context = context;
    }

    public Product GetById(int id) => _context.Set<Product>().Find(id);
    public IEnumerable<Product> GetAll() => _context.Set<Product>().ToList();

    public void Add(Product product)
    {
        _context.Set<Product>().Add(product);
        _context.SaveChanges();
    }

    public void Update(Product product)
    {
        _context.Set<Product>().Update(product);
        _context.SaveChanges();
    }

    public void Delete(int id)
    {
        var product = _context.Set<Product>().Find(id);
        if (product != null)
        {
            _context.Set<Product>().Remove(product);
            _context.SaveChanges();
        }
    }
}
```

### 3. Kullanımı
```csharp
var productRepo = new ProductRepository(dbContext);
var products = productRepo.GetAll();
```

---

## ✅ GENERIC REPOSITORY DESIGN PATTERN

### 1. Interface
```csharp
public interface IGenericRepository<T> where T : class
{
    IEnumerable<T> GetAll();
    T GetById(int id);
    void Add(T entity);
    void Update(T entity);
    void Delete(T entity);
    void Save();
}
```

### 2. Generic Repository
```csharp
public class GenericRepository<T> : IGenericRepository<T> where T : class
{
    private readonly DbContext _context;
    private readonly DbSet<T> _dbSet;

    public GenericRepository(DbContext context)
    {
        _context = context;
        _dbSet = _context.Set<T>();
    }

    public IEnumerable<T> GetAll() => _dbSet.ToList();
    public T GetById(int id) => _dbSet.Find(id);
    public void Add(T entity) => _dbSet.Add(entity);
    public void Update(T entity) => _dbSet.Update(entity);
    public void Delete(T entity) => _dbSet.Remove(entity);
    public void Save() => _context.SaveChanges();
}
```

### 3. Kullanımı
```csharp
IGenericRepository<Product> productRepo = new GenericRepository<Product>(dbContext);
productRepo.Add(new Product { Name = "Kalem" });
productRepo.Save();
```

---

## ⚖️ Karşılaştırma Tablosu

| Özellik                         | Klasik Repository                       | Generic Repository                         |
|----------------------------------|------------------------------------------|---------------------------------------------|
| Her Entity için Interface Gerekli | ✅                                        | ❌ (tek interface yeterlidir)               |
| Kod Tekrarı                     | Fazla                                    | Az                                          |
| Özelleştirme                    | Kolay (`IProductRepository`)             | Zor (miras alıp genişletmek gerekir)       |
| Kullanım Kolaylığı              | Karmaşık                                 | Basit                                       |
| CRUD Dışında Ek Metot Yazımı    | Kolay                                    | Zorlayıcı                                   |
| En İdeal Kullanım               | Büyük/özelleştirilmiş projeler           | Küçük/CRUD tabanlı projeler                |

---

## 💡 En İyi Uygulama (Hibrit Kullanım)

Generic yapıyı baz alırsın ama özel sorgular için entity’e özel repository eklersin:

```csharp
public class ProductRepository : GenericRepository<Product>
{
    public ProductRepository(DbContext context) : base(context) {}

    public IEnumerable<Product> GetByName(string name)
    {
        return _context.Set<Product>()
            .Where(p => p.Name.Contains(name))
            .ToList();
    }
}
```

Bu sayede kod tekrarını azaltırken entity'e özel işlemleri de sürdürebilirsin.