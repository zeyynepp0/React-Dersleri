# 🧭 curl Nedir? Ne İşe Yarar?

`curl` (Client URL), terminal (komut satırı) üzerinden internet ile veri alıp gönderme işlemlerini gerçekleştiren açık kaynaklı, çok yönlü bir araçtır. Web adresleri (URL) üzerinden dosya indirip yükleyebilir, HTTP istekleri (GET, POST, PUT, DELETE, PATCH vs.) gönderebilir ve gelen yanıtları inceleyebilirsin.

![curl logo](https://upload.wikimedia.org/wikipedia/commons/7/7e/Curl-logo.png)

---

## 🎯 curl'in Temel Amaçları

### 1. HTTP İstekleri Göndermek
Web API'lerine veri göndermek veya veri almak için kullanılır. Yaygın HTTP metodları:
- **GET:** Veri çekmek için kullanılır.
- **POST:** Yeni veri göndermek için kullanılır.
- **PUT:** Mevcut veriyi güncellemek için kullanılır.
- **DELETE:** Veri silmek için kullanılır.

#### ✅ Örnek: Basit GET İsteği
```bash
curl https://jsonplaceholder.typicode.com/posts
```
Bu komut, sahte bir API'den gönderiler listesini çeker.

#### ✅ Örnek: POST ile JSON Veri Gönderme
```bash
curl -X POST https://jsonplaceholder.typicode.com/posts \
  -H "Content-Type: application/json" \
  -d '{"title": "foo", "body": "bar", "userId": 1}'
```

### 2. API Testleri Yapmak
Yazılım geliştiriciler ve test uzmanları API’lerin doğru çalışıp çalışmadığını `curl` ile test eder. Bu testlerde kod yazmaya gerek yoktur.

#### 🔍 Örnek: Detaylı Yanıt Görmek
```bash
curl -v https://jsonplaceholder.typicode.com/posts/1
```

### 3. Dosya İndirme
İnternetten dosya indirmek için `curl` komutuna `-O` parametresi eklenir.

#### 📥 Örnek: Dosya İndirme
```bash
curl -O https://example.com/dosya.zip
```

### 4. Dosya Yükleme
Form verisi göndererek dosya yüklemek mümkündür.

#### 📤 Örnek: Dosya Yükleme
```bash
curl -F "file=@resim.jpg" http://localhost:3000/upload
```

### 5. Sunucu Yanıtlarını İncelemek
Sunucunun döndürdüğü başlık bilgileri (status code, content-type vb.) incelenebilir.

#### 📄 Örnek: Başlıkları Gösterme
```bash
curl -I https://example.com
```

---

## ✅ curl’in Avantajları

| Avantaj | Açıklama |
|--------|----------|
| ⚡ Hızlı | Kod yazmadan doğrudan test yapılabilir. |
| 💻 Arayüzsüz | Terminal veya script ile çalışır. GUI gerekmez. |
| 🔄 Çok yönlü | HTTP dışında FTP, SMTP gibi protokolleri destekler. |
| 🧪 Test dostu | REST API’lerini test etmek kolaydır. |
| 📦 Script dostu | Otomatikleştirme için idealdir (ör. cronjob içinde). |

---

## 📌 curl Nerelerde Kullanılır?

- **Frontend Geliştiriciler:** API uç noktalarının doğru çalıştığını test eder.
- **Backend Geliştiriciler:** Sunucuya veri gönderip almayı test eder.
- **DevOps:** Otomatik veri çekme/yükleme işlemleri için script'lerde kullanır.
- **Test Uzmanları:** API testi yaparken hızlı kontrol sağlar.

---

## 🌀 curl ve HTTP Arasındaki Fark

| Kavram | Açıklama |
|--------|----------|
| HTTP | Bir iletişim protokolüdür. Web üzerinden veri taşır. |
| curl | HTTP ve diğer protokolleri kullanan bir araçtır. |

**Özetle:** `curl`, HTTP üzerinden veri almak ve göndermek için kullanılan bir "araç"tır.

---

## 🛠 İleri Seviye Kullanımlar

### Token ile Kimlik Doğrulama
```bash
curl -H "Authorization: Bearer <token>" https://api.example.com/profile
```

### PUT Metodu Kullanmak
```bash
curl -X PUT https://jsonplaceholder.typicode.com/posts/1 \
  -H "Content-Type: application/json" \
  -d '{"title": "guncellenmis", "body": "icerik", "userId": 1}'
```

### DELETE Metodu Kullanmak
```bash
curl -X DELETE https://jsonplaceholder.typicode.com/posts/1
```

> 📝 Not: Sahte (mock) API'lerde silme işlemi gerçek anlamda gerçekleşmeyebilir. Yanıt her zaman 200 OK dönebilir.

---

## ❓ API Parametreleri Nereden Öğrenilir?

- API dokümantasyonları (Swagger UI, Redoc)
- Geliştirici ekipten alınan bilgiler
- Postman koleksiyonları
- JSON örnek çıktılar

---

## 🧪 curl vs Postman Karşılaştırması

| Özellik | curl | Postman |
|--------|------|---------|
| Hızlı test | ✅ | ✅ |
| Arayüz | ❌ | ✅ |
| Script desteği | ✅ | ❌ |
| JSON desteği | ✅ | ✅ |
| GUI bağımlılığı | ❌ | ✅ |

---

## 📦 Kurulum

### Linux
```bash
sudo apt update && sudo apt install curl
```

### MacOS
```bash
brew install curl
```

### Windows
Windows 10 ve üzeri sürümlerde `curl` yüklü gelir. CMD veya PowerShell ile kullanılabilir.

---

## 🎯 Örnek Uygulama: Sahte API Testi

```bash
curl -X POST https://jsonplaceholder.typicode.com/posts \
  -H "Content-Type: application/json" \
  -d '{"title": "Merhaba", "body": "Dünya", "userId": 5}'
```

**Beklenen Yanıt:**
```json
{
  "title": "Merhaba",
  "body": "Dünya",
  "userId": 5,
  "id": 101
}
```

---

## 🔚 Sonuç
`curl`, geliştiriciler, sistem yöneticileri ve test uzmanları için güçlü, hızlı ve pratik bir araçtır. Kod yazmaya gerek kalmadan birçok işlemi gerçekleştirebilir. JSON veri gönderimi, API testleri, dosya transferi gibi pek çok konuda seni Postman veya tarayıcıya muhtaç bırakmadan çalışmanı sağlar.

---

## 📚 Ek Kaynaklar
- [curl resmi sitesi](https://curl.se/)
- [curl dökümantasyonu](https://curl.se/docs/manpage.html)
- [JSONPlaceholder (test API)](https://jsonplaceholder.typicode.com/)