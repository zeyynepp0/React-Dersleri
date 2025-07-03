# React Temel Kavramlar – Açıklamalı Rehber

Bu belge, React ile uygulama geliştirmeye yeni başlayanlar için temel bileşenleri, veri aktarım yöntemlerini ve state yönetimini açıklar. Ayrıca kurulum ve proje oluşturma adımları da ayrıntılı olarak verilmiştir.

---

## 🎯 React Nedir?

React, kullanıcı arayüzleri (UI) oluşturmak için kullanılan popüler bir JavaScript kütüphanesidir. Sayfayı yeniden yüklemeden dinamik kullanıcı deneyimleri sunar. Temel olarak **Component**, **Props** ve **State** gibi yapı taşlarına sahiptir.

---

## 🧩 1. Component (Bileşen)

React uygulamaları bileşenler (components) tarafından oluşturulur. Bileşenler, kullanıcı arayüzünün farklı parçalarını temsil eder.

### 🛠️ Bileşen Türleri:

- **Fonksiyonel Bileşenler** (React 16.8 sonrası `hooks` ile popülerleşti)
- **Sınıf Tabanlı Bileşenler** (Klasik yöntem)

> Fonksiyonel bileşenler modern ve kullanımı daha kolaydır.

### 🔁 Avantaj:
Bir bileşeni tekrar tekrar çağırabilir, farklı yerlerde yeniden kullanabilirsiniz.

### 📦 Örnek Fonksiyonel Component:
```jsx
function Selamla() {
  return <h1>Merhaba React!</h1>;
}
```

---

## 📨 2. Props (Özellikler)

Props, bileşenler arasında veri taşımamızı sağlar. Bileşenin dış dünyadan aldığı değerleri ifade eder.

> Props, sadece okunabilir (read-only) yapıdadır.

### 📦 Örnek Props Kullanımı:
```jsx
function Selamla(props) {
  return <h1>Merhaba, {props.isim}!</h1>;
}
```

Kullanımı:
```jsx
<Selamla isim="Zeynep" />
```

---

## 🔄 3. State Management (Durum Yönetimi)

State (durum), bileşenin zamanla değişen verilerini tutar. Genellikle API'den veri alma işlemlerinde kullanılır.

### 📊 Temel State Durumları:

| Durum     | Açıklama                                             |
|-----------|------------------------------------------------------|
| `Loading` | Veri bekleniyor, animasyon gösterilebilir            |
| `Success` | Veri geldi, kullanıcıya gösterilir                   |
| `Error`   | Veri alınamadı, hata mesajı gösterilir               |

### 📘 `isLoading`, `data`, `error` gibi değişkenlerle yönetilir.

---

## 🧰 State Yönetimi Yöntemleri

### 1. `useState` + `useEffect`
- En temel yöntemdir
- Küçük projeler için yeterlidir
- State'ler manuel kontrol edilir

### 2. React Query (useQuery Hook)
- State yönetimini otomatikleştirir
- `isLoading`, `isSuccess`, `isError` gibi hazır değişkenler sunar
- Büyük projeler için idealdir

### 3. Redux Toolkit + createAsyncThunk
- `pending`, `fulfilled`, `rejected` durumları otomatik sağlanır
- `extraReducers` ile her durumu kontrol etme imkânı sağlar

### 4. SWR (Stale While Revalidate)
- Next.js ile uyumlu
- State'leri otomatik yönetir

---

## ⚙️ Kurulum Aşamaları

### 1. Visual Studio Code Kurulumu
Kod yazmak ve projeyi yönetmek için önerilen editör.

### 2. Node.js Kurulumu
React projeleri için gereklidir.

Komutlarla kontrol:
```bash
node -v    # Sürüm kontrol: 22.17.0
npm -v     # Sürüm kontrol: 10.9.2
```

> `npm`, paket yöneticisidir. Node.js ile birlikte kurulur.

---

## 🚀 Vite ile React Projesi Oluşturmak

Vite, hızlı ve modern bir build aracıdır.

### Komutlar:
```bash
npm create vite@latest
cd 1.giris
npm install
npm run dev
```

> Bu adımlar sonunda local sunucuda React uygulamanız çalışır hâle gelir.

---

## 🎨 Örnek: React Icons Yüklemek

```bash
cd 1.giris
npm install react-icons
```

> Komutlar, proje klasörünün içinden çalıştırılmalıdır.

---

## ✅ Özet

| Terim        | Açıklama                                        |
|--------------|-------------------------------------------------|
| Component    | UI parçalarını temsil eder                      |
| Props        | Component'e dışarıdan veri geçmek için kullanılır|
| State        | Component içinde değişken veri tutar            |
| useState     | React'te state yönetimi için kullanılır         |
| useEffect    | Yan etkileri yönetmek için (veri çekme vb.)     |

