
# JSON Server, REST API ve Axios Kullanımı (Detaylı Rehber)

Bu doküman, `json-server`, `Axios`, `fetch API` ve `REST API` konularını kapsamlı bir şekilde açıklar. Terminal komutları ve örnek senaryolarla desteklenmiştir.

Bu rehberde, **REST API** kavramı ile birlikte `JSON Server` kullanarak sahte bir backend nasıl oluşturulur adım adım gösterilecektir. Ayrıca `Axios` ve `Fetch API` ile bu veriler üzerinde nasıl işlemler yapılabileceği detaylıca açıklanacaktır.

---

## 📌 1. PowerShell'de Script İzinlerini Açmak

Windows üzerinde bazı komutlar çalışmazsa şu komutu yönetici terminalde çalıştırın:

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

---

## 🌐 2. REST API Nedir?

**REST (Representational State Transfer)**, istemci ve sunucu arasında veri alışverişi yapmayı sağlayan bir mimaridir. REST API ise bu mimariyi kullanarak farklı sistemlerin HTTP protokolü üzerinden iletişim kurmasını sağlar.

| Metot | Amaç             | Açıklama                         |
|-------|------------------|----------------------------------|
| GET   | Veri alma        | Belirli veya tüm verileri çeker |
| POST  | Yeni veri ekleme | Sunucuya yeni veri gönderir      |
| PUT   | Veri güncelleme  | Var olan veriyi tamamen değiştirir |
| DELETE| Veri silme       | Veriyi kalıcı olarak siler       |

---

## 🧰 3. JSON Server Kurulumu

### 🌍 Global Kurulum:

```bash
npm install -g json-server
```

### 📁 Yerel Kurulum:

```bash
npm install json-server
```

Kurulum sonrası sürüm kontrolü:

```bash
json-server --version
```

---

## 🗂️ 4. Sahte API Oluşturma

`db.json` adında bir dosya oluşturun ve aşağıdaki gibi örnek veri ekleyin:

```json
{
  "user": [
    { "id": 1, "name": "Zeynep", "password": "123", "postId": 1 }
  ]
}
```

Sunucuyu başlatmak için:

```bash
json-server --watch src/db.json --port 3005
```
> Bu komut ile `db.json` dosyası 3005 portu üzerinden izlenmeye başlar.

### Erişilebilecek endpointler:

- Tüm kullanıcılar: `http://localhost:3005/user`
- ID ile kullanıcı: `http://localhost:3005/user/1`
- Filtreli kullanıcı: `http://localhost:3005/user?id=1`

---

Bu işlem sonrası API uç noktası şu şekilde olur:

```
GET     http://localhost:3005/user
GET     http://localhost:3005/user/1
POST    http://localhost:3005/user
PUT     http://localhost:3005/user/1
DELETE  http://localhost:3005/user/1
```

---

## 📦 5. Axios Kurulumu

Projeye Axios eklemek için:

```bash
npm install axios
```
###App.jsx dosyasına ekleme
```bash
import axios from "axios";
```
---

## 📌 6. Axios ile CRUD İşlemleri

### 🔍 Tüm Kullanıcıları Getirme
```js
const getAllUsers = async () => {
  const response = await axios.get("http://localhost:3005/user");
  console.log(response.data);
};
```

### 🔍 ID’ye Göre Kullanıcı Getirme
```js
const getUserById = async (id) => {
  const response = await axios.get(`http://localhost:3005/user/${id}`);
  console.log(response.data);
};
```

### ➕ Yeni Kullanıcı Ekleme (POST)
```js
const newUser = { name: "Ela", password: "987" };
await axios.post("http://localhost:3005/user", newUser);
```

### ✏️ Kullanıcı Güncelleme (PUT)
```js
const updatedUser = { name: "Ali", password: "Elma123" };
await axios.put("http://localhost:3005/user/1", updatedUser);
```

### ❌ Kullanıcı Silme (DELETE)
```js
await axios.delete("http://localhost:3005/user/1");
```

---

## 🔄 Zincirleme Veri Çekme Örneği

1. Önce bir kullanıcıdan `postId` çekilir.
2. Sonra `jsonplaceholder` API'den ilgili post alınır.

```js
const getUserBy = async (userId) => {
  const response = await axios.get(`http://localhost:3005/user/${userId}`);
  return response.data.postId;
};

const getPostById = async (postId) => {
  const response = await axios.get(`https://jsonplaceholder.typicode.com/posts/${postId}`);
  return response.data;
};

const getPost = async () => {
  const postId = await getUserBy(1);
  const postData = await getPostById(postId);
  console.log(postData);
};
```

---

## 🛠️ Komut Tablosu

| Amaç                        | Komut                                                |
|-----------------------------|-------------------------------------------------------|
| JSON Server kurulumu        | `npm install -g json-server`                         |
| Sürüm kontrolü              | `json-server --version`                              |
| Sunucu başlatma             | `json-server --watch src/db.json --port 3005`        |
| Axios kurulumu              | `npm install axios`                                  |
| JSONPlaceholder örneği      | `https://jsonplaceholder.typicode.com/posts/1`       |

---

## 🔚 Sonuç

Bu rehberde, frontend projelerinde sahte verilerle çalışmak için `json-server` ve `Axios` kullanımını detaylıca öğrendiniz. Artık veri çekme, güncelleme, ekleme ve silme işlemlerini REST API üzerinden kolayca gerçekleştirebilirsiniz. 🎯
