# Yeşildere Belediyesi Web Sitesi

## 📋 Proje Hakkında
Yeşildere Belediyesi için modern, responsive ve yönetilebilir bir web sitesi projesidir. Site, belediye hizmetlerini, duyurularını ve etkinliklerini vatandaşlara ulaştırmayı amaçlamaktadır.

## 🚀 Özellikler
- Responsive tasarım (Mobile-first yaklaşımı)
- Modern ve kullanıcı dostu arayüz
- Kapsamlı admin paneli
- SEO uyumlu yapı
- Güvenli altyapı

### Ana Modüller
- 📰 Haberler
- 📅 Etkinlikler
- 📢 Duyurular
- 📝 Blog
- 🏘️ Mahalle Bilgileri
- 👥 Muhtar Bilgileri
- 🏛️ İlçe Hakkında

## 🛠️ Teknoloji Yığını

### Backend
- PHP 8.2+
- MySQL 8.0+
- Apache 2.4+

### Frontend
- HTML5
- CSS3
- JavaScript (ES6+)
- Bootstrap 5.3
- jQuery 3.7

### Paketler ve Kütüphaneler
```json
{
    "dependencies": {
        "bootstrap": "^5.3.0",
        "jquery": "^3.7.0",
        "@fortawesome/fontawesome-free": "^6.4.0",
        "swiper": "^10.0.0",
        "aos": "^2.3.4",
        "tinymce": "^6.0.0",
        "datatables.net-bs5": "^1.13.0",
        "chart.js": "^4.0.0"
    }
}
```

## 📁 Proje Yapısı
```
yesildere/
├── admin/             # Admin panel dosyaları
├── assets/           # Statik dosyalar
│   ├── css/         # CSS dosyaları
│   ├── js/          # JavaScript dosyaları
│   ├── img/         # Görsel dosyaları
│   └── uploads/     # Yüklenen dosyalar
├── includes/         # PHP include dosyaları
├── config/          # Yapılandırma dosyaları
└── templates/       # Şablon dosyaları
```

## ⚙️ Kurulum

### Sistem Gereksinimleri
- PHP 8.2+
- MySQL 8.0+
- Apache 2.4+
- SSL Sertifikası
- Minimum 2GB RAM
- 20GB Disk Alanı

### Kurulum Adımları

1. Repoyu klonlayın
```bash
git clone https://github.com/mukou78/yesildere.git
```

2. Bağımlılıkları yükleyin
```bash
composer install
npm install
```

3. Veritabanını oluşturun
```bash
mysql -u root -p
CREATE DATABASE yesildere_bel CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

4. Veritabanı tablolarını oluşturun
```bash
php migrate.php
```

5. Örnek verileri yükleyin (opsiyonel)
```bash
php seed.php
```

6. Config dosyasını düzenleyin
```bash
cp config/config.example.php config/config.php
# config.php dosyasını düzenleyin
```

## 🔒 Güvenlik
- JWT tabanlı kimlik doğrulama
- CSRF koruması
- XSS koruması
- SQL injection koruması
- Güvenli dosya yükleme sistemi
- Rate limiting
- SSL/TLS zorunluluğu

## 🔍 SEO
- Semantic HTML yapısı
- Meta etiketleri yönetimi
- Sitemap.xml
- Robots.txt
- SEO dostu URL yapısı

## 💾 Veritabanı Şeması
Ana tablolar:
- users (Kullanıcılar)
- news (Haberler)
- events (Etkinlikler)
- announcements (Duyurular)
- neighborhoods (Mahalleler)
- muhtars (Muhtarlar)
- blog_posts (Blog Yazıları)
- categories (Kategoriler)
- media (Medya)
- district_info (İlçe Bilgileri)

## 📝 Geliştirme Kuralları

### Kod Standartları
- PSR-4 autoloading standardı
- PSR-12 kodlama standardı
- BEM metodolojisi (CSS)
- ESLint (JavaScript)

### Git Commit Kuralları
```
feat: yeni özellik
fix: hata düzeltmesi
docs: dokümantasyon
style: kod formatı
refactor: kod yenileme
test: test ekleme/düzenleme
```

## 🚀 Deployment

### Deployment Kontrol Listesi
- [ ] Tüm formlar test edildi
- [ ] Responsive kontrolleri yapıldı
- [ ] SEO meta etiketleri kontrol edildi
- [ ] Güvenlik testleri yapıldı
- [ ] Performans optimizasyonu yapıldı
- [ ] Tarayıcı uyumluluk testleri yapıldı

### Deployment Ortamları
1. Geliştirme (Development)
2. Test
3. Staging
4. Production

## 🔄 Bakım ve Güncelleme
- Günlük veritabanı yedekleme
- Haftalık güvenlik taraması
- Aylık performans analizi
- 3 aylık sistem güncellemeleri

## 📈 Monitoring
- Sayfa yüklenme süreleri
- Sunucu kaynak kullanımı
- Veritabanı performansı
- Hata oranları

## 📄 Lisans
Bu proje özel lisans altında geliştirilmektedir. Tüm hakları Yeşildere Belediyesi'ne aittir.

## 👥 İletişim
Proje ile ilgili sorularınız için:
- 📧 Email: info@yesildere.com.tr
- 🌐 Website: https://www.yesildere.com.tr
- 📞 Telefon: xxx xxx xx xx 
