# RFC 02: API Endpoints

## 1. Kullanıcı ve Kimlik Doğrulama Endpoints

### 1.1 Giriş
```http
POST /api/v1/auth/login
```
```json
{
    "email": "string",
    "password": "string"
}
```

### 1.2 Token Yenileme
```http
POST /api/v1/auth/refresh
```
```json
{
    "refresh_token": "string"
}
```

### 1.3 Çıkış
```http
POST /api/v1/auth/logout
```

### 1.4 Şifre Sıfırlama İsteği
```http
POST /api/v1/auth/forgot-password
```
```json
{
    "email": "string"
}
```

### 1.5 Şifre Sıfırlama
```http
POST /api/v1/auth/reset-password
```
```json
{
    "token": "string",
    "password": "string",
    "password_confirmation": "string"
}
```

### 1.6 Şifre Değiştirme
```http
POST /api/v1/auth/change-password
```
```json
{
    "current_password": "string",
    "new_password": "string",
    "new_password_confirmation": "string"
}
```

### 1.7 Kullanıcı Listesi
```http
GET /api/v1/users
```
Query Parametreleri:
- page (int, default: 1)
- limit (int, default: 10)
- role (string: admin|editor|moderator)
- status (boolean: active|inactive)

### 1.8 Kullanıcı Detayı
```http
GET /api/v1/users/{id}
```

### 1.9 Kullanıcı Oluşturma
```http
POST /api/v1/users
```
```json
{
    "username": "string",
    "email": "string",
    "password": "string",
    "role": "string",
    "is_active": "boolean"
}
```

### 1.10 Kullanıcı Güncelleme
```http
PUT /api/v1/users/{id}
```
```json
{
    "username": "string",
    "email": "string",
    "role": "string",
    "is_active": "boolean"
}
```

### 1.11 Kullanıcı Silme
```http
DELETE /api/v1/users/{id}
```

## 2. Haber Endpoints

### 2.1 Haber Listesi
```http
GET /api/v1/news
```
Query Parametreleri:
- page (int, default: 1)
- limit (int, default: 10)
- category (string)
- status (string: published|draft|archived)
- featured (boolean)

### 2.2 Haber Detayı
```http
GET /api/v1/news/{id}
```

### 2.3 Haber Oluşturma
```http
POST /api/v1/news
```
```json
{
    "title": "string",
    "content": "string",
    "category_id": "integer",
    "image_url": "string",
    "status": "string",
    "is_featured": "boolean"
}
```

### 2.4 Haber Güncelleme
```http
PUT /api/v1/news/{id}
```

### 2.5 Haber Silme
```http
DELETE /api/v1/news/{id}
```

## 3. Etkinlik Endpoints

### 3.1 Etkinlik Listesi
```http
GET /api/v1/events
```
Query Parametreleri:
- page (int, default: 1)
- limit (int, default: 10)
- status (string: upcoming|ongoing|completed|cancelled)
- start_date (date)
- end_date (date)

### 3.2 Etkinlik Detayı
```http
GET /api/v1/events/{id}
```

### 3.3 Etkinlik Oluşturma
```http
POST /api/v1/events
```
```json
{
    "title": "string",
    "description": "string",
    "location": "string",
    "start_date": "datetime",
    "end_date": "datetime",
    "capacity": "integer",
    "registration_required": "boolean"
}
```

### 3.4 Etkinlik Güncelleme
```http
PUT /api/v1/events/{id}
```
```json
{
    "title": "string",
    "description": "string",
    "location": "string",
    "start_date": "datetime",
    "end_date": "datetime",
    "capacity": "integer",
    "registration_required": "boolean"
}
```

### 3.5 Etkinlik Silme
```http
DELETE /api/v1/events/{id}
```

## 4. Duyuru Endpoints

### 4.1 Duyuru Listesi
```http
GET /api/v1/announcements
```
Query Parametreleri:
- page (int, default: 1)
- limit (int, default: 10)
- type (string: general|tender|council|emergency)
- importance (string: low|medium|high)

### 4.2 Duyuru Detayı
```http
GET /api/v1/announcements/{id}
```

### 4.3 Duyuru Oluşturma
```http
POST /api/v1/announcements
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

### 4.4 Duyuru Güncelleme
```http
PUT /api/v1/announcements/{id}
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

### 4.5 Duyuru Silme
```http
DELETE /api/v1/announcements/{id}
```

## 5. Mahalle Endpoints

### 5.1 Mahalle Listesi
```http
GET /api/v1/neighborhoods
```

### 5.2 Mahalle Detayı
```http
GET /api/v1/neighborhoods/{id}
```

### 5.3 Mahalle Oluşturma
```http
POST /api/v1/neighborhoods
```
```json
{
    "name": "string",
    "description": "string",
    "population": "integer",
    "area_km2": "decimal",
    "postal_code": "string"
}
```

### 5.3 Mahalle Güncelleme
```http
PUT /api/v1/neighborhoods/{id}
```
```json
{
    "name": "string",
    "description": "string",
    "population": "integer",
    "area_km2": "decimal",
    "postal_code": "string"
}
```

### 5.4 Mahalle Silme
```http
DELETE /api/v1/neighborhoods/{id}
```

## 6. Muhtar Endpoints

### 6.1 Muhtar Listesi
```http
GET /api/v1/muhtars
```
Query Parametreleri:
- neighborhood_id (integer)

### 6.2 Muhtar Detayı
```http
GET /api/v1/muhtars/{id}
```

### 6.3 Muhtar Oluşturma
```http
POST /api/v1/muhtars
```
```json
{
    "neighborhood_id": "integer",
    "name": "string",
    "phone": "string",
    "email": "string",
    "office_address": "string",
    "term_start_date": "date",
    "term_end_date": "date"
}
```

### 6.4 Muhtar Güncelleme
```http
PUT /api/v1/muhtars/{id}
```
```json
{
    "neighborhood_id": "integer",
    "name": "string",
    "phone": "string",
    "email": "string",
    "office_address": "string",
    "term_start_date": "date",
    "term_end_date": "date"
}
```

### 6.5 Muhtar Silme
```http
DELETE /api/v1/muhtars/{id}
```

## 7. Blog Endpoints

### 7.1 Blog Yazı Listesi
```http
GET /api/v1/blog
```
Query Parametreleri:
- page (int, default: 1)
- limit (int, default: 10)
- category (string)
- status (string: published|draft|archived)

### 7.2 Blog Yazı Detayı
```http
GET /api/v1/blog/{id}
```

### 7.3 Blog Yazısı Oluşturma
```http
POST /api/v1/blog
```
```json
{
    "title": "string",
    "content": "string",
    "category_id": "integer",
    "featured_image": "string",
    "status": "string"
}
```

### 7.4 Blog Yazısı Güncelleme
```http
PUT /api/v1/blog/{id}
```
```json
{
    "title": "string",
    "content": "string",
    "category_id": "integer",
    "featured_image": "string",
    "status": "string"
}
```

### 7.5 Blog Yazısı Silme
```http
DELETE /api/v1/blog/{id}
```

## 8. İlçe Bilgileri Endpoints

### 8.1 İlçe Bilgileri Listesi
```http
GET /api/v1/district-info
```
Query Parametreleri:
- type (string: history|geography|demographics|culture)

### 8.2 İlçe Bilgisi Detayı
```http
GET /api/v1/district-info/{id}
```

### 8.3 İlçe Bilgisi Oluşturma
```http
POST /api/v1/district-info
```
```json
{
    "title": "string",
    "content": "string",
    "type": "string"
}
```

### 8.4 İlçe Bilgisi Güncelleme
```http
PUT /api/v1/district-info/{id}
```
```json
{
    "title": "string",
    "content": "string",
    "type": "string"
}
```

### 8.5 İlçe Bilgisi Silme
```http
DELETE /api/v1/district-info/{id}
```

## 9. Medya Endpoints

### 9.1 Medya Yükleme
```http
POST /api/v1/media/upload
```
Multipart form data:
- file: binary
- type: string (image|document|video|other)
- title: string
- description: string (optional)

### 9.2 Medya Listesi
```http
GET /api/v1/media
```
Query Parametreleri:
- page (int, default: 1)
- limit (int, default: 20)
- type (string: image|document|video|other)

### 9.3 Medya Detayı
```http
GET /api/v1/media/{id}
```

### 9.4 Medya Güncelleme
```http
PUT /api/v1/media/{id}
```
```json
{
    "title": "string",
    "description": "string",
    "type": "string"
}
```

### 9.5 Medya Silme
```http
DELETE /api/v1/media/{id}
```

## 10. Site Ayarları Endpoints

### 10.1 Tüm Ayarları Listele
```http
GET /api/v1/settings
```
Query Parametreleri:
- group (string: general|seo|contact|appearance)
- is_public (boolean)

### 10.2 Ayar Grubu Detayı
```http
GET /api/v1/settings/{group}
```

### 10.3 Ayar Güncelleme
```http
PUT /api/v1/settings/{group}/{key}
```
```json
{
    "value": "string"
}
```

### 10.4 Toplu Ayar Güncelleme
```http
PUT /api/v1/settings/{group}
```
```json
{
    "settings": [
        {
            "key": "site_title",
            "value": "Yeni Site Başlığı"
        },
        {
            "key": "site_description",
            "value": "Yeni Site Açıklaması"
        }
    ]
}
```

### 10.5 Logo/Görsel Yükleme
```http
POST /api/v1/settings/upload
```
Multipart form data:
- file: binary
- type: string (header_logo|footer_logo|favicon) 