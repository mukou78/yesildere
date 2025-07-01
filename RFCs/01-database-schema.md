# RFC 01: Veritabanı Şeması

## 1. Kullanıcılar (users)
```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    role ENUM('admin', 'editor', 'moderator') NOT NULL,
    is_active BOOLEAN DEFAULT true,
    last_login DATETIME,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

## 2. Haberler (news)
```sql
CREATE TABLE news (
    id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(255) NOT NULL,
    slug VARCHAR(255) UNIQUE NOT NULL,
    content TEXT NOT NULL,
    image_url VARCHAR(255),
    category_id INT,
    author_id INT,
    status ENUM('draft', 'published', 'archived') DEFAULT 'draft',
    view_count INT DEFAULT 0,
    is_featured BOOLEAN DEFAULT false,
    published_at DATETIME,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES categories(id),
    FOREIGN KEY (author_id) REFERENCES users(id)
);
```

## 3. Etkinlikler (events)
```sql
CREATE TABLE events (
    id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(255) NOT NULL,
    slug VARCHAR(255) UNIQUE NOT NULL,
    description TEXT NOT NULL,
    image_url VARCHAR(255),
    location VARCHAR(255) NOT NULL,
    start_date DATETIME NOT NULL,
    end_date DATETIME NOT NULL,
    status ENUM('upcoming', 'ongoing', 'completed', 'cancelled') DEFAULT 'upcoming',
    capacity INT,
    registration_required BOOLEAN DEFAULT false,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

## 4. Duyurular (announcements)
```sql
CREATE TABLE announcements (
    id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(255) NOT NULL,
    slug VARCHAR(255) UNIQUE NOT NULL,
    content TEXT NOT NULL,
    type ENUM('general', 'tender', 'council', 'emergency') NOT NULL,
    importance ENUM('low', 'medium', 'high') DEFAULT 'medium',
    start_date DATETIME NOT NULL,
    end_date DATETIME,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

## 5. Mahalleler (neighborhoods)
```sql
CREATE TABLE neighborhoods (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    population INT,
    area_km2 DECIMAL(10,2),
    postal_code VARCHAR(10),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

## 6. Muhtarlar (muhtars)
```sql
CREATE TABLE muhtars (
    id INT PRIMARY KEY AUTO_INCREMENT,
    neighborhood_id INT NOT NULL,
    name VARCHAR(100) NOT NULL,
    phone VARCHAR(20),
    email VARCHAR(100),
    office_address TEXT,
    term_start_date DATE NOT NULL,
    term_end_date DATE,
    photo_url VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (neighborhood_id) REFERENCES neighborhoods(id)
);
```

## 7. Blog Yazıları (blog_posts)
```sql
CREATE TABLE blog_posts (
    id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(255) NOT NULL,
    slug VARCHAR(255) UNIQUE NOT NULL,
    content TEXT NOT NULL,
    author_id INT NOT NULL,
    category_id INT,
    status ENUM('draft', 'published', 'archived') DEFAULT 'draft',
    featured_image VARCHAR(255),
    view_count INT DEFAULT 0,
    published_at DATETIME,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (author_id) REFERENCES users(id),
    FOREIGN KEY (category_id) REFERENCES categories(id)
);
```

## 8. Kategoriler (categories)
```sql
CREATE TABLE categories (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL,
    slug VARCHAR(50) UNIQUE NOT NULL,
    description TEXT,
    parent_id INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (parent_id) REFERENCES categories(id)
);
```

## 9. Medya (media)
```sql
CREATE TABLE media (
    id INT PRIMARY KEY AUTO_INCREMENT,
    file_name VARCHAR(255) NOT NULL,
    file_path VARCHAR(255) NOT NULL,
    file_type ENUM('image', 'document', 'video', 'other') NOT NULL,
    mime_type VARCHAR(100) NOT NULL,
    file_size INT NOT NULL,
    uploaded_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (uploaded_by) REFERENCES users(id)
);
```

## 10. İlçe Bilgileri (district_info)
```sql
CREATE TABLE district_info (
    id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(255) NOT NULL,
    content TEXT NOT NULL,
    type ENUM('history', 'geography', 'demographics', 'culture') NOT NULL,
    last_updated_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (last_updated_by) REFERENCES users(id)
);
```

## 11. Site Ayarları (settings)
```sql
CREATE TABLE settings (
    id INT PRIMARY KEY AUTO_INCREMENT,
    group_name ENUM('general', 'seo', 'contact', 'appearance') NOT NULL,
    key_name VARCHAR(100) NOT NULL,
    value TEXT,
    input_type ENUM('text', 'textarea', 'image', 'color', 'select', 'boolean') NOT NULL,
    options TEXT NULL,
    is_public BOOLEAN DEFAULT true,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    UNIQUE KEY unique_setting (group_name, key_name)
);

-- Varsayılan ayarlar
INSERT INTO settings (group_name, key_name, value, input_type) VALUES
-- Genel Ayarlar
('general', 'site_title', 'Yeşildere Belediyesi', 'text'),
('general', 'site_description', 'Yeşildere Belediyesi Resmi Web Sitesi', 'textarea'),
('general', 'header_logo', 'uploads/logo.png', 'image'),
('general', 'favicon', 'uploads/favicon.ico', 'image'),
('general', 'footer_logo', 'uploads/footer-logo.png', 'image'),
('general', 'phone', '+90 xxx xxx xx xx', 'text'),
('general', 'email', 'info@yesildere.bel.tr', 'text'),
('general', 'address', 'Yeşildere Belediyesi, xxxxx', 'textarea'),
('general', 'facebook_url', '', 'text'),
('general', 'twitter_url', '', 'text'),
('general', 'instagram_url', '', 'text'),
('general', 'youtube_url', '', 'text'),
('general', 'google_analytics', '', 'textarea'),
('general', 'maintenance_mode', '0', 'boolean'),

-- SEO Ayarları
('seo', 'meta_title', 'Yeşildere Belediyesi', 'text'),
('seo', 'meta_description', 'Yeşildere Belediyesi Resmi Web Sitesi', 'textarea'),
('seo', 'meta_keywords', 'belediye, yeşildere', 'textarea'),
('seo', 'robots_txt', 'User-agent: *\nAllow: /', 'textarea'),

-- İletişim Ayarları
('contact', 'map_coordinates', '41.xxx,29.xxx', 'text'),
('contact', 'working_hours', '09:00 - 18:00', 'text'),
('contact', 'contact_email', 'contact@yesildere.bel.tr', 'text'),

-- Görünüm Ayarları
('appearance', 'primary_color', '#007bff', 'color'),
('appearance', 'secondary_color', '#6c757d', 'color'),
('appearance', 'font_family', 'Roboto', 'select'),
('appearance', 'header_style', 'default', 'select'),
('appearance', 'footer_style', 'default', 'select');
```

## İndeksler

```sql
-- Performans optimizasyonu için önerilen indeksler
CREATE INDEX idx_news_status ON news(status);
CREATE INDEX idx_events_dates ON events(start_date, end_date);
CREATE INDEX idx_announcements_dates ON announcements(start_date, end_date);
CREATE INDEX idx_blog_posts_status ON blog_posts(status);
CREATE INDEX idx_categories_parent ON categories(parent_id);
CREATE INDEX idx_media_type ON media(file_type);
``` 