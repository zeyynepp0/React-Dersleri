# 💻 ASP.NET Nedir?

**ASP.NET**, Microsoft tarafından geliştirilen bir web uygulama geliştirme platformudur. Dinamik web siteleri, web servisleri, RESTful API’ler ve modern uygulamalar geliştirmek için kullanılır.

ASP.NET aslında bir **şemsiye teknolojidir**, yani içinde birçok alt teknoloji barındırır:

### ASP.NET İçindeki Geliştirme Modelleri:
- **ASP.NET Web Forms** (eski sistem)
- **ASP.NET MVC** (Model-View-Controller)
- **ASP.NET Web API** (API servisleri için)
- **ASP.NET Core** (yeni nesil platform bağımsız yapı)

---

# 📐 MVC Nedir? (ASP.NET MVC)

**MVC**: Model – View – Controller mimari desenine dayalı bir geliştirme modelidir.

| Katman     | Görevi |
|------------|--------|
| 🧠 **Model**     | Verileri ve iş kurallarını temsil eder. |
| 🎨 **View**      | Kullanıcının gördüğü HTML/CSS arayüzünü sunar. |
| 🎮 **Controller** | Kullanıcıdan gelen istekleri karşılar, modeli işler ve view ile sonucu sunar. |

🔸 **Amaç**: Kodun daha düzenli, test edilebilir ve yönetilebilir olmasıdır.

---

# 🧩 ASP.NET MVC, Web API ve ASP.NET Core Karşılaştırması

## 1️⃣ ASP.NET MVC

###  Nedir?
- Microsoft’un .NET Framework üzerinde çalışan klasik web uygulama modelidir.
- **MVC desenini kullanır**.
- Dinamik HTML sayfaları üretmek için kullanılır.
- **Sunucu-taraflı (server-side) render** yapar.

### 🟢 Kullanım Alanı
- Yönetim panelleri, iç sistemler, şirket içi uygulamalar

### 🔴 Zayıf Nokta
- JSON API üretimi zordur.
- Modern frontend framework'leriyle kullanımı sınırlıdır.

---

## 2️⃣ ASP.NET Web API

### 🇹🇷 Nedir?
- RESTful web servisleri geliştirmek için tasarlanmıştır.
- ASP.NET MVC’ye çok benzer ama **JSON/XML veri döner, HTML değil**.
- .NET Framework üzerinde çalışır.

### 🟢 Kullanım Alanı
- React, Angular, Vue.js gibi frontend uygulamalarına veri sağlayan servisler

### 🔴 Zayıf Nokta
- MVC’den ayrı bir yapıdadır.
- UI sayfa üretimi içermez.

---

## 3️⃣ ASP.NET Core

### 🇹🇷 Nedir?
- Microsoft’un geliştirdiği yeni nesil **platform bağımsız** (cross-platform) framework’tür.
- Hem MVC hem Web API yapısını **tek bir çatıda birleştirir**.
- Windows, Linux ve macOS üzerinde çalışabilir.
- Yüksek performanslı ve modülerdir.

### 🟢 Kullanım Alanı
- Web siteleri
- RESTful API servisleri
- Microservice uygulamaları
- Bulut tabanlı sistemler
- Blazor ve SignalR gibi modern yaklaşımlar

### 🟢 Artı Özellikler
- Modern dependency injection (bağımlılık yönetimi)
- Minimal API yapısı
- Razor Pages ve Blazor desteği

---

# ⚖️ ASP.NET Yapılarının Karşılaştırma Tablosu

| Özellik              | ASP.NET MVC         | ASP.NET Web API     | ASP.NET Core             |
|----------------------|---------------------|----------------------|---------------------------|
| Çalışma Ortamı       | .NET Framework      | .NET Framework       | .NET Core (.NET 5/6/7+)   |
| HTML Sayfa Üretimi   | ✅                  | ❌                   | ✅                        |
| JSON API Desteği     | 🔸 Zayıf            | ✅                  | ✅                        |
| MVC Desteği          | ✅                  | 🔸 Sınırlı           | ✅                        |
| API + MVC birleşik   | ❌                  | ❌                   | ✅                        |
| Cross-Platform       | ❌ Sadece Windows   | ❌ Sadece Windows    | ✅                        |
| Modern Performans    | 🔸 Orta             | 🔸 Orta              | ✅ Yüksek                 |

---

# 🎯 Sonuç

- Eğer sadece HTML sayfaları üretmek istiyorsan → **ASP.NET MVC**
- Eğer sadece API (JSON veri) sunmak istiyorsan → **ASP.NET Web API**
- Eğer modern, hızlı ve çapraz platform bir çözüm arıyorsan → **ASP.NET Core** ✅

---

# 📚 Ek Kaynaklar

- [ASP.NET Resmi Sitesi](https://dotnet.microsoft.com/en-us/apps/aspnet)
- [ASP.NET Core Belgeleri](https://learn.microsoft.com/en-us/aspnet/core/)
- [MVC Deseni Nedir?](https://en.wikipedia.org/wiki/Model–view–controller)