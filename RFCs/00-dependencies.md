# RFC Bağımlılıkları ve İlişkileri

## RFC 01: Veritabanı Şeması
- **Bağımlılıklar:** Yok (İlk RFC)
- **İlişkili RFC'ler:**
  - RFC 02: API Endpoints (Veritabanı tablolarına göre endpoint'ler tasarlandı)
  - RFC 03: Frontend Mimarisi (Veritabanı yapısına göre form ve listeleme komponentleri oluşturuldu)
  - RFC 04: Güvenlik (Veritabanı güvenliği ve veri doğrulama kuralları)

## RFC 02: API Endpoints
- **Bağımlılıklar:** 
  - RFC 01: Veritabanı Şeması (Tablo yapıları ve ilişkiler)
- **İlişkili RFC'ler:**
  - RFC 03: Frontend Mimarisi (API endpoint'lerini kullanan frontend komponentleri)
  - RFC 04: Güvenlik (API güvenliği ve yetkilendirme)
  - RFC 05: API Dokümantasyonu (API endpoint'lerinin detaylı dokümantasyonu)

## RFC 03: Frontend Mimarisi
- **Bağımlılıklar:**
  - RFC 01: Veritabanı Şeması (Form ve liste yapıları)
  - RFC 02: API Endpoints (Veri alışverişi için kullanılan endpoint'ler)
- **İlişkili RFC'ler:**
  - RFC 04: Güvenlik (Frontend güvenlik önlemleri)
  - RFC 05: API Dokümantasyonu (API kullanım örnekleri)

## RFC 04: Güvenlik
- **Bağımlılıklar:**
  - RFC 01: Veritabanı Şeması (Veri güvenliği kuralları)
  - RFC 02: API Endpoints (API güvenlik protokolleri)
  - RFC 03: Frontend Mimarisi (Frontend güvenlik önlemleri)
- **İlişkili RFC'ler:**
  - RFC 05: API Dokümantasyonu (Güvenlik protokollerinin dokümantasyonu)

## RFC 05: API Dokümantasyonu
- **Bağımlılıklar:**
  - RFC 02: API Endpoints (Dokümante edilecek endpoint'ler)
  - RFC 04: Güvenlik (Güvenlik protokolleri ve kuralları)
- **İlişkili RFC'ler:**
  - RFC 03: Frontend Mimarisi (API kullanım örnekleri)

## İlerleme Sırası

1. RFC 01: Veritabanı Şeması
   - Temel veri yapısını oluşturur
   - Diğer tüm RFC'ler için temeoluştururl 

2. RFC 02: API Endpoints
   - Veritabanı şemasına göre API'leri tasarlar
   - Frontend ve güvenlik için temel oluşturur

3. RFC 04: Güvenlik
   - Veritabanı ve API güvenliğini sağlar
   - Frontend geliştirmeden önce güvenlik kurallarını belirler

4. RFC 03: Frontend Mimarisi
   - Güvenli API'leri kullanarak frontend'i oluşturur
   - Kullanıcı arayüzünü tasarlar

5. RFC 05: API Dokümantasyonu
   - Tüm sistemin dokümantasyonunu oluşturur
   - Geliştirici kılavuzunu hazırlar

## Önemli Bağlantı Noktaları

1. **Veri Yapısı ve Güvenlik**
   - RFC 01 → RFC 04: Veritabanı güvenliği
   - RFC 02 → RFC 04: API güvenliği
   - RFC 03 → RFC 04: Frontend güvenliği

2. **API ve Frontend Entegrasyonu**
   - RFC 02 → RFC 03: API endpoint'lerinin frontend'de kullanımı
   - RFC 04 → RFC 03: Güvenlik önlemlerinin frontend'de uygulanması

3. **Dokümantasyon ve Entegrasyon**
   - RFC 02 → RFC 05: API endpoint dokümantasyonu
   - RFC 04 → RFC 05: Güvenlik protokolleri dokümantasyonu
   - RFC 03 → RFC 05: Frontend entegrasyon örnekleri 