# RFC 03: Frontend Mimarisi

## 1. Teknoloji Yığını

### 1.1 Temel Teknolojiler
- HTML5
- CSS3
- JavaScript (ES6+)
- Bootstrap 5.3
- jQuery 3.7

### 1.2 Paketler
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

## 2. Dizin Yapısı

```
assets/
├── css/
│   ├── main.css
│   ├── components/
│   │   ├── header.css
│   │   ├── footer.css
│   │   ├── sidebar.css
│   │   └── cards.css
│   └── pages/
│       ├── home.css
│       ├── news.css
│       └── events.css
├── js/
│   ├── main.js
│   ├── components/
│   │   ├── slider.js
│   │   ├── gallery.js
│   │   └── forms.js
│   └── pages/
│       ├── home.js
│       ├── news.js
│       └── events.js
└── img/
    ├── logo/
    ├── icons/
    └── photos/
```

## 3. Sayfa Şablonları

### 3.1 Ana Şablon
```html
<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}{% endblock %} - Yeşildere Belediyesi</title>
    <!-- CSS -->
    <link rel="stylesheet" href="/assets/css/main.css">
    {% block css %}{% endblock %}
</head>
<body>
    {% include 'header.html' %}
    
    <main class="container">
        {% block content %}{% endblock %}
    </main>

    {% include 'footer.html' %}
    
    <!-- JS -->
    <script src="/assets/js/main.js"></script>
    {% block js %}{% endblock %}
</body>
</html>
```

### 3.2 Responsive Breakpoints
```css
/* Bootstrap 5 breakpoints */
$grid-breakpoints: (
  xs: 0,
  sm: 576px,
  md: 768px,
  lg: 992px,
  xl: 1200px,
  xxl: 1400px
);
```

## 4. Komponentler

### 4.1 Header
```html
<header class="main-header">
    <nav class="navbar navbar-expand-lg">
        <div class="container">
            <a class="navbar-brand" href="/">
                <img src="/assets/img/logo.png" alt="Yeşildere Belediyesi">
            </a>
            <!-- Responsive menü -->
        </div>
    </nav>
</header>
```

### 4.2 Footer
```html
<footer class="main-footer">
    <div class="container">
        <div class="row">
            <!-- İletişim bilgileri -->
            <!-- Hızlı linkler -->
            <!-- Sosyal medya -->
        </div>
    </div>
</footer>
```

### 4.3 Admin Panel Komponentleri
```html
<!-- Site Ayarları Formu -->
<div class="settings-form">
    <div class="nav nav-tabs">
        <button class="nav-link active" data-bs-toggle="tab" data-bs-target="#general">
            Genel Ayarlar
        </button>
        <button class="nav-link" data-bs-toggle="tab" data-bs-target="#seo">
            SEO Ayarları
        </button>
        <button class="nav-link" data-bs-toggle="tab" data-bs-target="#contact">
            İletişim Ayarları
        </button>
        <button class="nav-link" data-bs-toggle="tab" data-bs-target="#appearance">
            Görünüm Ayarları
        </button>
    </div>

    <div class="tab-content">
        <!-- Genel Ayarlar -->
        <div class="tab-pane fade show active" id="general">
            <form id="generalSettingsForm">
                <div class="mb-3">
                    <label>Site Başlığı</label>
                    <input type="text" name="site_title" class="form-control">
                </div>
                <div class="mb-3">
                    <label>Site Açıklaması</label>
                    <textarea name="site_description" class="form-control"></textarea>
                </div>
                <div class="mb-3">
                    <label>Header Logo</label>
                    <input type="file" name="header_logo" class="form-control">
                </div>
                <!-- Diğer genel ayarlar -->
            </form>
        </div>

        <!-- SEO Ayarları -->
        <div class="tab-pane fade" id="seo">
            <form id="seoSettingsForm">
                <div class="mb-3">
                    <label>Meta Başlık</label>
                    <input type="text" name="meta_title" class="form-control">
                </div>
                <!-- Diğer SEO ayarları -->
            </form>
        </div>

        <!-- İletişim Ayarları -->
        <div class="tab-pane fade" id="contact">
            <form id="contactSettingsForm">
                <div class="mb-3">
                    <label>Telefon</label>
                    <input type="text" name="phone" class="form-control">
                </div>
                <!-- Diğer iletişim ayarları -->
            </form>
        </div>

        <!-- Görünüm Ayarları -->
        <div class="tab-pane fade" id="appearance">
            <form id="appearanceSettingsForm">
                <div class="mb-3">
                    <label>Ana Renk</label>
                    <input type="color" name="primary_color" class="form-control">
                </div>
                <!-- Diğer görünüm ayarları -->
            </form>
        </div>
    </div>
</div>
```

## 5. Sayfa Yapıları

### 5.1 Ana Sayfa
```html
{% extends 'base.html' %}

{% block content %}
<section class="hero">
    <!-- Slider -->
</section>

<section class="news">
    <!-- Haberler -->
</section>

<section class="events">
    <!-- Etkinlikler -->
</section>

<section class="announcements">
    <!-- Duyurular -->
</section>
{% endblock %}
```

### 5.2 Haber Listesi
```html
{% extends 'base.html' %}

{% block content %}
<div class="news-list">
    <div class="filters">
        <!-- Kategori filtreleri -->
    </div>
    
    <div class="grid">
        {% for news in news_list %}
        <div class="news-card">
            <!-- Haber kartı -->
        </div>
        {% endfor %}
    </div>
    
    <div class="pagination">
        <!-- Sayfalama -->
    </div>
</div>
{% endblock %}
```

## 6. JavaScript Modülleri

### 6.1 Slider Modülü
```javascript
class Slider {
    constructor(element, options) {
        this.element = element;
        this.options = {
            autoplay: true,
            interval: 5000,
            ...options
        };
        this.init();
    }

    init() {
        // Slider başlatma
    }

    next() {
        // Sonraki slide
    }

    prev() {
        // Önceki slide
    }
}
```

### 6.2 Form Validasyonu
```javascript
class FormValidator {
    constructor(form) {
        this.form = form;
        this.init();
    }

    init() {
        this.form.addEventListener('submit', this.handleSubmit.bind(this));
    }

    handleSubmit(e) {
        if (!this.validate()) {
            e.preventDefault();
        }
    }

    validate() {
        // Form doğrulama
    }
}
```

### 6.3 Ayarlar Modülü
```javascript
class SettingsManager {
    constructor() {
        this.forms = {
            general: document.getElementById('generalSettingsForm'),
            seo: document.getElementById('seoSettingsForm'),
            contact: document.getElementById('contactSettingsForm'),
            appearance: document.getElementById('appearanceSettingsForm')
        };
        this.init();
    }

    init() {
        // Form submit olaylarını dinle
        Object.keys(this.forms).forEach(group => {
            this.forms[group].addEventListener('submit', (e) => {
                e.preventDefault();
                this.saveSettings(group);
            });
        });

        // Ayarları yükle
        this.loadSettings();
    }

    async loadSettings() {
        try {
            const response = await fetch('/api/v1/settings');
            const settings = await response.json();
            this.populateForms(settings);
        } catch (error) {
            console.error('Ayarlar yüklenemedi:', error);
        }
    }

    async saveSettings(group) {
        try {
            const formData = new FormData(this.forms[group]);
            const settings = Array.from(formData.entries()).map(([key, value]) => ({
                key,
                value
            }));

            await fetch(`/api/v1/settings/${group}`, {
                method: 'PUT',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ settings })
            });

            alert('Ayarlar kaydedildi!');
        } catch (error) {
            console.error('Ayarlar kaydedilemedi:', error);
        }
    }

    populateForms(settings) {
        settings.forEach(setting => {
            const form = this.forms[setting.group_name];
            if (form) {
                const input = form.querySelector(`[name="${setting.key_name}"]`);
                if (input) {
                    input.value = setting.value;
                }
            }
        });
    }
}
```

## 7. CSS Metodolojisi

### 7.1 BEM Yapısı
```css
/* Block */
.news-card {}

/* Element */
.news-card__title {}
.news-card__image {}

/* Modifier */
.news-card--featured {}
```

### 7.2 Utility Classes
```css
/* Margin utilities */
.mt-1 { margin-top: 0.25rem; }
.mb-2 { margin-bottom: 0.5rem; }

/* Text utilities */
.text-primary { color: var(--primary-color); }
.text-center { text-align: center; }
```

## 8. Performans Optimizasyonu

### 8.1 Resim Optimizasyonu
- WebP formatı kullanımı
- Lazy loading
- Responsive images
- Image sprites

### 8.2 CSS/JS Optimizasyonu
- Minification
- Concatenation
- Critical CSS
- Async/Defer script loading

### 8.3 Caching Stratejisi
- Browser caching
- Service workers
- Local storage kullanımı

## 9. SEO Optimizasyonu

### 9.1 Meta Etiketleri
```html
<meta name="description" content="...">
<meta name="keywords" content="...">
<meta property="og:title" content="...">
<meta property="og:description" content="...">
<meta property="og:image" content="...">
```

### 9.2 Semantic HTML
```html
<article>
<section>
<nav>
<header>
<footer>
<main>
<aside>
```

## 10. Erişilebilirlik

### 10.1 ARIA Etiketleri
```html
<button aria-label="Menüyü aç">
<img alt="Açıklayıcı metin">
<div role="alert">
```

### 10.2 Klavye Navigasyonu
```javascript
// Focus yönetimi
// Tab index
// Keyboard shortcuts
```

## 11. Dinamik Site Ayarları

### 11.1 CSS Değişkenleri
```css
:root {
    --primary-color: var(--setting-primary-color, #007bff);
    --secondary-color: var(--setting-secondary-color, #6c757d);
    --font-family: var(--setting-font-family, 'Roboto');
}
```

### 11.2 Ayarları Yükleme
```javascript
class SiteSettings {
    static async loadPublicSettings() {
        try {
            const response = await fetch('/api/v1/settings?is_public=true');
            const settings = await response.json();
            
            // CSS değişkenlerini güncelle
            settings.forEach(setting => {
                if (setting.group_name === 'appearance') {
                    document.documentElement.style.setProperty(
                        `--setting-${setting.key_name}`,
                        setting.value
                    );
                }
            });

            // Meta etiketlerini güncelle
            const seoSettings = settings.filter(s => s.group_name === 'seo');
            seoSettings.forEach(setting => {
                const meta = document.querySelector(`meta[name="${setting.key_name}"]`);
                if (meta) {
                    meta.setAttribute('content', setting.value);
                }
            });
        } catch (error) {
            console.error('Site ayarları yüklenemedi:', error);
        }
    }
}

// Sayfa yüklendiğinde ayarları yükle
document.addEventListener('DOMContentLoaded', () => {
    SiteSettings.loadPublicSettings();
});
``` 