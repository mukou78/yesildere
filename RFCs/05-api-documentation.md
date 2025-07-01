# RFC 05: API Dokümantasyonu

## 1. Genel Bilgiler

### 1.1 Base URL
```
https://api.yesildere.com.tr/v1
```

### 1.2 Kimlik Doğrulama
- JWT (JSON Web Token) kullanılacak
- Token geçerlilik süresi: 24 saat
- Refresh token süresi: 7 gün

### 1.3 İstek Formatı
```http
Content-Type: application/json
Authorization: Bearer <token>
```

### 1.4 Yanıt Formatı
```json
{
    "status": true|false,
    "data": {},
    "message": "İşlem mesajı",
    "errors": []
}
```

## 2. Endpoints

### 2.1 Kullanıcı İşlemleri

#### Login
```http
POST /auth/login
```
```json
{
    "email": "string",
    "password": "string"
}
```

#### Token Yenileme
```http
POST /auth/refresh
```
```json
{
    "refresh_token": "string"
}
```

### 2.2 Haberler

#### Haber Listesi
```http
GET /news
```
Query Parametreleri:
- page (int, default: 1)
- limit (int, default: 10)
- category (string)
- status (string: published|draft|archived)

#### Haber Detayı
```http
GET /news/{id}
```

#### Haber Oluşturma
```http
POST /news
```
```json
{
    "title": "string",
    "content": "string",
    "category_id": "integer",
    "image_url": "string",
    "status": "string"
}
```

### 2.3 Etkinlikler

#### Etkinlik Listesi
```http
GET /events
```
Query Parametreleri:
- page (int, default: 1)
- limit (int, default: 10)
- status (string: upcoming|ongoing|completed|cancelled)

#### Etkinlik Detayı
```http
GET /events/{id}
```

#### Etkinlik Oluşturma
```http
POST /events
```
```json
{
    "title": "string",
    "description": "string",
    "location": "string",
    "start_date": "datetime",
    "end_date": "datetime",
    "capacity": "integer"
}
```

### 2.4 Duyurular

#### Duyuru Listesi
```http
GET /announcements
```
Query Parametreleri:
- page (int, default: 1)
- limit (int, default: 10)
- type (string: general|tender|council|emergency)

#### Duyuru Detayı
```http
GET /announcements/{id}
```

#### Duyuru Oluşturma
```http
POST /announcements
```
```json
{
    "title": "string",
    "content": "string",
    "type": "string",
    "importance": "string",
    "start_date": "datetime",
    "end_date": "datetime"
}
```

## 3. Hata Kodları

### 3.1 HTTP Durum Kodları
- 200: Başarılı
- 201: Oluşturuldu
- 400: Geçersiz İstek
- 401: Yetkisiz Erişim
- 403: Erişim Reddedildi
- 404: Bulunamadı
- 500: Sunucu Hatası

### 3.2 Özel Hata Kodları
```json
{
    "status": false,
    "error": {
        "code": "AUTH001",
        "message": "Geçersiz token"
    }
}
```

## 4. Rate Limiting
- IP başına: 1000 istek/saat
- Token başına: 2000 istek/saat

## 5. Güvenlik

### 5.1 SSL/TLS
- Minimum TLS 1.2
- HTTPS zorunluluğu

### 5.2 CORS Politikası
```json
{
    "allowed_origins": [
        "https://yesildere.com.tr",
        "https://admin.yesildere.com.tr"
    ],
    "allowed_methods": ["GET", "POST", "PUT", "DELETE"],
    "allowed_headers": ["Content-Type", "Authorization"]
}
```

## 6. Versiyon Kontrolü
- URI tabanlı versiyonlama (/v1, /v2)
- Eski versiyonlar 6 ay desteklenecek
- Versiyon geçişleri 1 ay önceden duyurulacak

## 7. Cache Stratejisi
- Redis kullanılacak
- Cache süresi:
  - Statik veriler: 24 saat
  - Dinamik veriler: 5 dakika
- Cache-Control header kullanımı

## 8. API Kullanım Örnekleri

### 8.1 Haber Listesi
```javascript
fetch('https://api.yesildere.com.tr/v1/news?page=1&limit=10', {
    headers: {
        'Authorization': 'Bearer <token>'
    }
})
.then(response => response.json())
.then(data => console.log(data));
```

### 8.2 Etkinlik Oluşturma
```javascript
fetch('https://api.yesildere.com.tr/v1/events', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer <token>'
    },
    body: JSON.stringify({
        title: 'Yeni Etkinlik',
        description: 'Etkinlik açıklaması',
        start_date: '2024-04-01T10:00:00',
        end_date: '2024-04-01T18:00:00'
    })
})
.then(response => response.json())
.then(data => console.log(data));
``` 