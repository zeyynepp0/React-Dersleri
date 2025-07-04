# 🔁 CI/CD Nedir? Süreci ve Örnek Yapılandırma

## 🚀 CI/CD Nedir?

**CI/CD**, yazılım geliştirme sürecinde kodun otomatik olarak test edilmesi, derlenmesi ve canlıya alınması için kullanılan bir yaklaşımdır.

- **CI (Continuous Integration)** → Sürekli Entegrasyon: Kod her güncellenişte test edilir.
- **CD (Continuous Delivery / Continuous Deployment)** → Sürekli Teslim / Sürekli Yayın: Test edilen kod staging ya da production ortamına otomatik aktarılır.

---

## 🔁 CI/CD Süreci Nasıl İşler?

1. ✅ Kod yazılır → Yeni özellik veya hata düzeltmesi eklenir.
2. ✅ Kod Git repo'ya push edilir → GitHub, GitLab, Bitbucket vb.
3. ✅ CI sistemi tetiklenir → GitLab CI, Jenkins, GitHub Actions vb.
4. ✅ Kod test ve build edilir → Otomatik testler çalışır.
5. ✅ Testler geçerse:
   - Continuous Delivery → staging ortamına geçer.
   - Continuous Deployment → production'a otomatik olarak alınır.

---

## ⚙️ Örnek `.gitlab-ci.yml` (Node.js İçin)

```yaml
stages:
  - build
  - test
  - deploy

variables:
  NODE_ENV: production

before_script:
  - npm install

build:
  stage: build
  script:
    - echo "Build aşaması"
    - npm run build

test:
  stage: test
  script:
    - echo "Testler çalıştırılıyor"
    - npm test

deploy:
  stage: deploy
  script:
    - echo "Deploy ediliyor"
    - ssh user@server "cd /var/www/project && git pull && npm install && pm2 restart app"
  only:
    - main
```

---

## 🎯 Neden CI/CD Kullanılır?

### 🔁 1. Süreçleri Otomatikleştirir
- Build, test ve deploy işlemleri otomatikleşir.
- ⏱️ **Kazanç:** Zaman tasarrufu, hızlı teslimat.

### 🧪 2. Hataları Erken Yakalar
- Otomatik testler sayesinde hatalı kod erken bulunur.
- 🔍 **Kazanç:** Kaliteli kod, daha az canlı hata.

### 💡 3. Hızlı ve Sürekli Yayın
- Commit sonrası otomatik olarak test/staging/canlıya geçiş yapılabilir.
- 🚀 **Kazanç:** Güvenli, sık ve hızlı yayın süreci.

### 👥 4. Takım Çalışmasına Uygundur
- Her geliştiricinin katkısı otomatik test edilir.
- 🤝 **Kazanç:** Tutarlılık ve sürdürülebilirlik.

### 🔐 5. Canlıya Çıkarken Güvenlik Artar
- Testlerden geçmiş kod canlıya alınır.
- 🔐 **Kazanç:** Daha güvenli ve kararlı sistemler.

### 📊 6. Süreç Gözlemlenebilir
- CI/CD araçları log ve rapor sunar.
- 📈 **Kazanç:** Hata takibi ve gelişmiş denetim.

---

## 📌 Avantajlar Tablosu

| Avantaj | Açıklama |
|--------|----------|
| ✅ Hızlı Teslim | Kodlar hızlıca canlıya alınır. |
| ✅ Hataların Erken Tespiti | Kod merge edilmeden önce test edilir. |
| ✅ Daha Az İnsan Hatası | Yayın süreci otomatikleştirilmiştir. |
| ✅ Takım Uyumu | Herkes aynı kalite kontrolünden geçer. |

---

## 🛠️ Popüler CI/CD Araçları

- **GitHub Actions**
- **GitLab CI/CD**
- **Jenkins**
- **CircleCI**
- **Travis CI**
- **Bitbucket Pipelines**

---

## 🔚 Sonuç

CI/CD, yazılım süreçlerini daha **hızlı**, **güvenilir**, **test edilebilir** ve **otomatik** hale getirir. Her yazılım projesi için modern geliştirme yaşam döngüsünün vazgeçilmez bir parçasıdır.