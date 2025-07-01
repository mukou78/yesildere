# Yeşildere Belediyesi Web Sitesi

## 📌 Proje Hakkında
Yeşildere Belediyesi için geliştirilmiş modern, responsive ve yönetilebilir bir web sitesi projesidir. Bu proje, belediye hizmetlerini dijital ortamda vatandaşlara ulaştırmak ve belediye ile vatandaş arasındaki iletişimi güçlendirmek amacıyla tasarlanmıştır.

## 🚀 Özellikler

### 🌐 Ziyaretçi Arayüzü
- **Ana Sayfa**
  - Dinamik slider/banner sistemi
  - Öne çıkan haberler bölümü
  - Son duyurular listesi
  - Güncel etkinlikler takvimi

- **Mahalle Bilgileri**
  - Detaylı mahalle profilleri
  - Muhtar bilgileri ve iletişim
  - Mahalle fotoğraf galerileri
  - Konum bilgileri

- **Haber ve Duyurular**
  - Kategorize edilmiş haber sistemi
  - Resim galerisi entegrasyonu
  - Tarih bazlı filtreleme
  - Sosyal medya paylaşım özellikleri

- **Etkinlik Yönetimi**
  - Gelecek/geçmiş etkinlik listeleri
  - Etkinlik takvimi görünümü
  - Detaylı etkinlik sayfaları

### ⚙️ Admin Paneli
- **Kullanıcı Yönetimi**
  - Rol tabanlı yetkilendirme
  - Güvenli oturum yönetimi
  - Kullanıcı işlem logları

- **İçerik Yönetimi**
  - Haber/duyuru yönetimi
  - Etkinlik organizasyonu
  - Medya kütüphanesi
  - Sayfa içerik düzenleme

- **Site Ayarları**
  - Genel ayarlar (logo, başlık, iletişim)
  - SEO optimizasyonları
  - Sosyal medya entegrasyonu
  - Görünüm özelleştirmeleri

## 🛠 Teknik Altyapı

### Kullanılan Teknolojiler
- **Backend:** PHP 8.x
- **Frontend:** HTML5, CSS3, JavaScript
- **Veritabanı:** MySQL 8.x
- **Cache:** Redis
- **Frontend Framework:** Bootstrap 5
- **JavaScript Library:** jQuery

### Sistem Gereksinimleri
- PHP >= 8.0
- MySQL >= 8.0
- Redis >= 6.0
- Apache/Nginx Web Server
- mod_rewrite enabled
- PHP Extensions:
  - PDO PHP Extension
  - MySQL PHP Extension
  - GD PHP Extension
  - JSON PHP Extension
  - Redis PHP Extension

## 🚀 Kurulum

1. Repoyu klonlayın:
```bash
git clone https://github.com/mukou78/yesildere.git
cd belediye-web
```

2. Veritabanını oluşturun:
```bash
mysql -u root -p
CREATE DATABASE yesildere_belediye;
```

3. Yapılandırma dosyasını oluşturun:
```bash
cp includes/config/config.example.php includes/config/config.php
```

4. Gerekli PHP paketlerini yükleyin:
```bash
composer install
```

5. Veritabanı tablolarını oluşturun:
```bash
php artisan migrate
```

6. Örnek verileri yükleyin:
```bash
php artisan db:seed
```

## 📁 Proje Yapısı

```
yesildere/
├── admin/                 # Admin panel dosyaları
│   ├── controllers/      # Admin kontrolcüleri
│   ├── views/           # Admin görünümleri
│   └── assets/          # Admin panel özel dosyaları
├── api/                  # API dosyaları
│   ├── v1/             # API version 1
│   │   ├── controllers/  # API kontrolcüleri
│   │   ├── models/      # API modelleri
│   │   ├── routes/      # API rotaları
│   │   ├── middleware/  # API middleware'leri
│   │   └── helpers/     # API yardımcı fonksiyonları
│   └── docs/           # API dokümantasyonu
├── assets/              # Statik dosyalar
└── includes/            # PHP include dosyaları
```

## 🔒 Güvenlik Önlemleri
- SQL Injection koruması
- XSS (Cross-site scripting) koruması
- CSRF (Cross-site request forgery) koruması
- JWT tabanlı API güvenliği
- Güvenli dosya yükleme sistemi
- Input validasyonu
- Prepared statements kullanımı

## 🌐 API Kullanımı

### Endpoint Yapısı
```
/api/v1/{resource}/{id?}
```

### Örnek İstekler

#### Haber Listesi
```http
GET /api/v1/news
```

#### Tek Haber Detayı
```http
GET /api/v1/news/{id}
```

#### Yeni Haber Ekleme
```http
POST /api/v1/news
```

### Response Format
```json
{
    "status": true|false,
    "data": {},
    "message": "İşlem mesajı",
    "errors": []
}
```

## 💻 Geliştirici Kılavuzu

### Kod Standartları

#### PHP
```php
// Sınıf isimleri PascalCase
class UserController {
    // Metot isimleri camelCase
    public function getUserData() {
        // Değişken isimleri camelCase
        $userData = [];
    }
}
```

#### JavaScript
```javascript
// Fonksiyon isimleri camelCase
function handleSubmit() {
    const formData = new FormData();
}
```

### Git Commit Kuralları
```
feat: yeni özellik
fix: hata düzeltmesi
docs: dokümantasyon
style: kod formatı
refactor: kod yenileme
test: test ekleme/düzenleme
```

## 🚀 Deployment Süreci

### Kontrol Listesi
- [ ] Tüm formlar test edildi
- [ ] Responsive kontroller yapıldı
- [ ] SEO meta etiketleri kontrol edildi
- [ ] Güvenlik testleri yapıldı
- [ ] Performans optimizasyonu yapıldı
- [ ] API endpoint'leri test edildi
- [ ] Veritabanı yedeklendi
- [ ] SSL sertifikası kontrol edildi
- [ ] Cache temizlendi

## 📈 Performans Optimizasyonu
- WebP formatında resim optimizasyonu
- JavaScript dosyaları sayfa sonunda yükleme
- CSS dosyaları header'da yükleme
- Redis cache kullanımı
- API rate limiting
- HTTP isteklerini minimize etme

## 🔍 SEO Optimizasyonu
- Semantic HTML kullanımı
- Sayfa bazlı meta etiketleri
- Alt tag optimizasyonu
- SEO dostu URL yapısı
- Otomatik sitemap.xml
- Robots.txt yönetimi

## 📱 Responsive Tasarım
```css
/* Bootstrap breakpoints */
$grid-breakpoints: (
    xs: 0,
    sm: 576px,
    md: 768px,
    lg: 992px,
    xl: 1200px,
    xxl: 1400px
);
```

## 🤝 Katkıda Bulunma
1. Fork'layın
2. Feature branch oluşturun (`git checkout -b feature/amazing-feature`)
3. Commit'leyin (`git commit -m 'feat: amazing feature'`)
4. Branch'e push yapın (`git push origin feature/amazing-feature`)
5. Pull Request oluşturun

## 📝 Lisans
Bu proje MIT lisansı altında lisanslanmıştır. Detaylar için [LICENSE](LICENSE) dosyasını inceleyebilirsiniz.

## 📞 İletişim
Yeşildere Belediyesi - info@yesildere.com.tr 
