# PHP Backend API Starter 🚀

A minimal, clean PHP backend starter kit with environment configuration, database setup, and modern API practices. Perfect for quickly starting new PHP projects with proper security and structure.

---

## ✨ Features

- 🔐 **Environment Configuration** with phpdotenv
- 🗄️ **Database Ready** with PDO connections
- 🌐 **CORS Enabled** APIs
- 📦 **Composer** dependency management
- 🎯 **Minimal Structure** - only 2 core files needed
- 🔧 **Easy to Extend** for any project type
- 🧪 **Testing Ready** with sample endpoints

---

## 🛠 Quick Start

### 1. Create & Setup
```bash
# Create project
composer create-project yourname/php-backend-starter my-project
cd my-project

# Or clone and install
git clone https://github.com/yourname/php-backend-starter.git
cd php-backend-starter
composer install
```

### 2. Configure Environment
```bash
# Copy and edit environment file
cp .env.example .env
```

### 3. Run & Test
```bash
# Test configuration
php test.php

# Start local server
php -S localhost:8000
```

---

## 📁 Project Structure

```
php-backend-starter/
├── .env                    # Environment variables
├── config.php              # Core configuration
├── composer.json           # Dependencies
├── api/
│   └── users.php          # Sample API endpoint
├── vendor/                 # Composer packages
└── README.md
```

---

## 🎯 Core Files

### `config.php` - Central Configuration
```php
<?php
require_once __DIR__ . '/vendor/autoload.php';

use Dotenv\Dotenv;

$dotenv = Dotenv::createImmutable(__DIR__);
$dotenv->load();

// Define database configuration
define('DB_HOST', $_ENV['DB_HOST']);
define('DB_NAME', $_ENV['DB_NAME']);
define('DB_USER', $_ENV['DB_USER']);
define('DB_PASS', $_ENV['DB_PASS']);
?>
```

### `api/users.php` - Sample Endpoint
```php
<?php
require_once '../config.php';

header("Content-Type: application/json");

try {
    $pdo = new PDO("mysql:host=".DB_HOST.";dbname=".DB_NAME, DB_USER, DB_PASS);
    
    $stmt = $pdo->query("SELECT * FROM users");
    $users = $stmt->fetchAll(PDO::FETCH_ASSOC);
    
    echo json_encode(['success' => true, 'data' => $users]);
    
} catch (PDOException $e) {
    echo json_encode(['success' => false, 'error' => 'Database error']);
}
?>
```

---

## ⚡ Usage Examples

### Frontend Integration
```javascript
// Fetch data from your PHP API
const response = await fetch('/api/users.php');
const data = await response.json();
console.log(data);
```

### Add New Endpoint
```php
<?php
// api/products.php
require_once '../config.php';

header("Content-Type: application/json");

// Your business logic here
echo json_encode(['message' => 'New endpoint working!']);
?>
```

---

## 🗃️ Database Setup

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## 🧪 Testing

```bash
# Test configuration
php test.php

# Test API endpoint
curl http://localhost:8000/api/users.php

# Test with POST
curl -X POST http://localhost:8000/api/users.php \
  -H "Content-Type: application/json" \
  -d '{"name":"John","email":"john@example.com"}'
```

---

## 🚀 Deployment Ready

- Environment-based configuration
- Secure credential management
- Production-ready error handling
- CORS configured for web apps
- Standardized JSON responses

---

## 📦 What's Included

| File | Purpose |
|------|---------|
| `config.php` | Central configuration loader |
| `.env` | Environment variables |
| `api/users.php` | Sample REST endpoint |
| `composer.json` | Dependency management |
| `test.php` | Configuration tester |

---

## 🔧 Customization

1. **Add environment variables** in `.env`
2. **Extend config.php** with new constants
3. **Create new endpoints** in `/api/` folder
4. **Add dependencies** via `composer require`

---

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🆘 Support

- 📖 [Documentation](#)
- 🐛 [Issues](#)
- 💬 [Discussions](#)

---

**Start your next PHP project in seconds, not hours!** ⚡

---

<div align="center">

### ⭐ Don't forget to star this repo if you find it useful!

</div>
