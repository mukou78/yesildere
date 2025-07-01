# RFC 04: Güvenlik Protokolleri

## 1. Kimlik Doğrulama ve Yetkilendirme

### 1.1 JWT (JSON Web Token)
```php
class JWTAuth {
    private $secret_key = 'your-256-bit-secret';
    private $token_expiry = 86400; // 24 saat
    private $refresh_token_expiry = 604800; // 7 gün

    public function generateToken($user_id) {
        $payload = [
            'user_id' => $user_id,
            'iat' => time(),
            'exp' => time() + $this->token_expiry
        ];
        return JWT::encode($payload, $this->secret_key);
    }
}
```

### 1.2 Rol Tabanlı Erişim Kontrolü (RBAC)
```php
class RoleManager {
    private $roles = [
        'admin' => ['all'],
        'editor' => ['create_post', 'edit_post', 'delete_post'],
        'moderator' => ['approve_comment', 'delete_comment']
    ];

    public function hasPermission($user_role, $permission) {
        return in_array($permission, $this->roles[$user_role]);
    }
}
```

## 2. Veri Güvenliği

### 2.1 SQL Injection Koruması
```php
class Database {
    public function query($sql, $params = []) {
        $stmt = $this->pdo->prepare($sql);
        return $stmt->execute($params);
    }
}

// Kullanım
$db->query("SELECT * FROM users WHERE email = ?", [$email]);
```

### 2.2 XSS Koruması
```php
function sanitizeOutput($data) {
    if (is_array($data)) {
        return array_map('sanitizeOutput', $data);
    }
    return htmlspecialchars($data, ENT_QUOTES, 'UTF-8');
}
```

### 2.3 CSRF Koruması
```php
class CSRFProtection {
    public function generateToken() {
        if (empty($_SESSION['csrf_token'])) {
            $_SESSION['csrf_token'] = bin2hex(random_bytes(32));
        }
        return $_SESSION['csrf_token'];
    }

    public function validateToken($token) {
        return hash_equals($_SESSION['csrf_token'], $token);
    }
}
```

## 3. Dosya Güvenliği

### 3.1 Güvenli Dosya Yükleme
```php
class FileUploader {
    private $allowed_types = ['jpg', 'jpeg', 'png', 'pdf'];
    private $max_size = 5242880; // 5MB

    public function upload($file) {
        // Dosya tipi kontrolü
        $ext = strtolower(pathinfo($file['name'], PATHINFO_EXTENSION));
        if (!in_array($ext, $this->allowed_types)) {
            throw new Exception('Geçersiz dosya tipi');
        }

        // Boyut kontrolü
        if ($file['size'] > $this->max_size) {
            throw new Exception('Dosya çok büyük');
        }

        // Güvenli dosya adı
        $new_name = uniqid() . '.' . $ext;
        
        // Dosyayı taşı
        move_uploaded_file($file['tmp_name'], 'uploads/' . $new_name);
    }
}
```

### 3.2 Dosya Tipi Doğrulama
```php
function validateFileType($file) {
    $finfo = finfo_open(FILEINFO_MIME_TYPE);
    $mime_type = finfo_file($finfo, $file['tmp_name']);
    finfo_close($finfo);

    $allowed_types = [
        'image/jpeg',
        'image/png',
        'application/pdf'
    ];

    return in_array($mime_type, $allowed_types);
}
```

## 4. Şifreleme ve Hash

### 4.1 Şifre Hash'leme
```php
class PasswordHasher {
    public function hash($password) {
        return password_hash($password, PASSWORD_ARGON2ID, [
            'memory_cost' => 65536,
            'time_cost' => 4,
            'threads' => 3
        ]);
    }

    public function verify($password, $hash) {
        return password_verify($password, $hash);
    }
}
```

### 4.2 Veri Şifreleme
```php
class Encryptor {
    private $key;
    private $cipher = "aes-256-gcm";

    public function encrypt($data) {
        $iv = random_bytes(12);
        $tag = '';
        
        $encrypted = openssl_encrypt(
            $data,
            $this->cipher,
            $this->key,
            OPENSSL_RAW_DATA,
            $iv,
            $tag
        );

        return base64_encode($iv . $tag . $encrypted);
    }
}
```

## 5. HTTP Güvenliği

### 5.1 Security Headers
```php
function setSecurityHeaders() {
    header("Strict-Transport-Security: max-age=31536000; includeSubDomains");
    header("X-Frame-Options: SAMEORIGIN");
    header("X-Content-Type-Options: nosniff");
    header("X-XSS-Protection: 1; mode=block");
    header("Content-Security-Policy: default-src 'self'");
    header("Referrer-Policy: strict-origin-when-cross-origin");
}
```

### 5.2 Rate Limiting
```php
class RateLimiter {
    private $redis;
    private $max_requests = 100;
    private $window = 3600; // 1 saat

    public function checkLimit($ip) {
        $key = "rate_limit:$ip";
        $current = $this->redis->get($key);

        if (!$current) {
            $this->redis->setex($key, $this->window, 1);
            return true;
        }

        if ($current >= $this->max_requests) {
            return false;
        }

        $this->redis->incr($key);
        return true;
    }
}
```

## 6. Session Güvenliği

### 6.1 Session Yapılandırması
```php
function configureSession() {
    ini_set('session.cookie_httponly', 1);
    ini_set('session.cookie_secure', 1);
    ini_set('session.cookie_samesite', 'Strict');
    ini_set('session.gc_maxlifetime', 3600);
    session_start();
}
```

### 6.2 Session Hijacking Koruması
```php
class SessionManager {
    public function regenerateSession() {
        if (isset($_SESSION['last_regeneration'])) {
            if (time() - $_SESSION['last_regeneration'] > 300) {
                session_regenerate_id(true);
                $_SESSION['last_regeneration'] = time();
            }
        } else {
            $_SESSION['last_regeneration'] = time();
        }
    }
}
```

## 7. Loglama ve Monitoring

### 7.1 Güvenlik Logları
```php
class SecurityLogger {
    public function logSecurityEvent($event_type, $details) {
        $log = [
            'timestamp' => date('Y-m-d H:i:s'),
            'event_type' => $event_type,
            'ip' => $_SERVER['REMOTE_ADDR'],
            'user_agent' => $_SERVER['HTTP_USER_AGENT'],
            'details' => $details
        ];
        
        // Log dosyasına yaz
        file_put_contents(
            'security.log',
            json_encode($log) . "\n",
            FILE_APPEND
        );
    }
}
```

### 7.2 Failed Login Attempts
```php
class LoginAttemptTracker {
    private $max_attempts = 5;
    private $lockout_time = 900; // 15 dakika

    public function recordFailedAttempt($ip) {
        $attempts = $this->getAttempts($ip);
        if ($attempts >= $this->max_attempts) {
            $this->lockAccount($ip);
            return false;
        }
        $this->incrementAttempts($ip);
        return true;
    }
}
```

## 8. Backup ve Recovery

### 8.1 Otomatik Yedekleme
```php
class DatabaseBackup {
    public function createBackup() {
        $filename = 'backup_' . date('Y-m-d_H-i-s') . '.sql';
        $command = "mysqldump -u {$this->user} -p{$this->pass} {$this->db} > backups/{$filename}";
        exec($command);
        
        // Şifrele
        $this->encryptBackup($filename);
    }
}
```

### 8.2 Yedek Rotasyonu
```php
class BackupRotation {
    private $max_backups = 30;

    public function rotate() {
        $backups = glob('backups/*.sql.enc');
        if (count($backups) > $this->max_backups) {
            array_map('unlink', array_slice($backups, 0, -$this->max_backups));
        }
    }
}
``` 