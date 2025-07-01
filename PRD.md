# Yeşildere Belediyesi Web Sitesi - PRD (Ürün Gereksinim Dokümanı)

## 1. Proje Özeti
Yeşildere Belediyesi için modern, responsive ve yönetilebilir bir web sitesi geliştirilecektir.

## 2. Teknik Altyapı
- Backend: PHP
- Frontend: HTML5, CSS3, JavaScript
- Framework/Kütüphaneler: 
  - Bootstrap 5 (Responsive tasarım için)
  - jQuery (JavaScript işlemleri için)
- Veritabanı: MySQL

## 3. Ana Özellikler

### 3.1 Ziyaretçi Arayüzü
1. **Ana Sayfa**
   - Slider/Banner alanı
   - Öne çıkan haberler
   - Son duyurular
   - Güncel etkinlikler

2. **Mahalleler**
   - 2 mahallenin detaylı bilgileri
   - Her mahalle için muhtar bilgileri
   - Mahalle fotoğrafları
   - İletişim bilgileri

3. **Haberler**
   - Kategorilendirilmiş haberler
   - Resim galerisi
   - Tarih bazlı filtreleme
   - Sosyal medya paylaşım butonları

4. **Etkinlikler**
   - Gelecek etkinlikler
   - Geçmiş etkinlikler
   - Etkinlik takvimi
   - Etkinlik detay sayfaları

5. **Blog**
   - Kategoriler
   - Yazı içerikleri
   - Yorum sistemi
   - Paylaşım özellikleri

6. **İlçe Hakkında**
   - Tarihçe
   - Coğrafi bilgiler
   - Demografik bilgiler
   - Kültürel değerler

7. **Duyurular**
   - Resmi duyurular
   - İhale duyuruları
   - Meclis kararları
   - Önemli bilgilendirmeler

### 3.2 Admin Paneli
1. **Kullanıcı Yönetimi**
   - Admin kullanıcı girişi
   - Şifre değiştirme
   - Yetkilendirme sistemi

2. **Site Ayarları**
   - Genel Ayarlar
     - Site başlığı
     - Site açıklaması
     - Site logosu (header)
     - Site favicon
     - Footer logosu
     - İletişim bilgileri (telefon, e-posta, adres)
     - Sosyal medya bağlantıları
     - Meta etiketleri
     - Google Analytics kodu
     - Bakım modu ayarı
   - SEO Ayarları
     - Default meta başlık
     - Default meta açıklama
     - Default meta anahtar kelimeler
     - Robots.txt düzenleme
     - Sitemap ayarları
   - İletişim Ayarları
     - Harita koordinatları
     - Çalışma saatleri
     - İletişim formu e-posta ayarları
   - Görünüm Ayarları
     - Site renk şeması
     - Font ayarları
     - Header stili
     - Footer stili

3. **İçerik Yönetimi**
   - Haber ekleme/düzenleme/silme
   - Etkinlik ekleme/düzenleme/silme
   - Blog yazısı ekleme/düzenleme/silme
   - Duyuru ekleme/düzenleme/silme
   - Mahalle bilgileri güncelleme
   - Muhtar bilgileri güncelleme
   - İlçe bilgileri yönetimi
     - Tarihçe düzenleme
     - Coğrafi bilgileri güncelleme
     - Demografik verileri güncelleme
     - Kültürel değerleri düzenleme
     - İlçe fotoğraf galerisi yönetimi

4. **Medya Yönetimi**
   - Resim yükleme/düzenleme/silme
   - Dosya yükleme/düzenleme/silme
   - Galeri yönetimi

## 4. Teknik Gereksinimler

### 4.1 Responsive Tasarım
- Mobil öncelikli tasarım
- Tüm ekran boyutlarına uyumluluk
- Touch-friendly arayüz

### 4.2 Performans
- Hızlı sayfa yüklenme süreleri
- Optimize edilmiş görseller
- Önbellek sistemi

### 4.3 Güvenlik
- SQL injection koruması
- XSS koruması
- CSRF koruması
- Güvenli dosya yükleme sistemi

### 4.4 SEO
- SEO dostu URL yapısı
- Meta etiketleri yönetimi
- Sitemap.xml
- Robots.txt

## 5. Veritabanı Yapısı (Ana Tablolar)
- users (Kullanıcılar)
- news (Haberler)
- events (Etkinlikler)
- announcements (Duyurular)
- neighborhoods (Mahalleler)
- muhtars (Muhtarlar)
- blog_posts (Blog Yazıları)
- categories (Kategoriler)
- media (Medya)

## 6. Tahmini Zaman Planı
1. Tasarım ve Frontend Geliştirme: 2 hafta
2. Backend Geliştirme: 3 hafta
3. Admin Panel Geliştirme: 2 hafta
4. Test ve Düzeltmeler: 1 hafta
Toplam: 8 hafta 