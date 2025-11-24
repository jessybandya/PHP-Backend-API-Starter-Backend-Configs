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
- 💻 **VM Ready** with editor commands

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
# Copy environment template
cp .env.example .env

# Edit .env file (choose your editor):
nano .env                    # Simple terminal editor
vim .env                     # Vim editor
code .env                    # VS Code (if installed)
sudo nano .env              # If permission issues
```

### 3. Run & Test
```bash
# Test configuration
php test.php

# Start local server
php -S localhost:8000
```

---

## 🖥️ VM/Server Editor Commands

### Quick .env Editing
```bash
# Using Nano (recommended for beginners)
nano .env

# Using Vim
vim .env

# Using VS Code (if installed)
code .env

# Using default system editor
edit .env
```

### Save & Exit Commands

**For Nano:**
```bash
nano .env
# Ctrl + O → Save | Ctrl + X → Exit
```

**For Vim:**
```bash
vim .env
# Press 'i' to insert/edit
# Esc → :wq → Enter (Save & Exit)
# Esc → :q! → Enter (Exit without saving)
```

**For Vi:**
```bash
vi .env
# Same commands as Vim
```

### Permission Fixes (if needed)
```bash
# If you get permission errors:
sudo chmod 644 .env
sudo nano .env

# Or change ownership:
sudo chown $USER:$USER .env
nano .env
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

## ⚡ Quick Setup Script

### `setup.sh` - Complete Automation
```bash
#!/bin/bash
echo "🚀 Setting up PHP Backend Starter..."

# Create project structure
mkdir -p php-backend-starter/api
cd php-backend-starter

# Install dependencies
composer require vlucas/phpdotenv

# Create .env file
cat > .env << 'EOL'
DB_HOST=localhost
DB_NAME=myapp_db
DB_USER=root
DB_PASS=password
APP_NAME="My PHP API"
APP_ENV=development
EOL

echo "✅ Setup complete!"
echo "📝 Edit your .env file: nano .env"
echo "🧪 Test configuration: php test.php"
```

### Run the setup:
```bash
chmod +x setup.sh
./setup.sh
```

---

## 🔧 Environment Configuration

### Edit .env File:
```bash
# Open for editing
nano .env

# Sample .env content:
DB_HOST=localhost
DB_NAME=myapp_db
DB_USER=root
DB_PASS=your_password_here
APP_NAME="My Awesome API"
APP_ENV=development
```

### Verify Configuration:
```bash
# Test if config loads correctly
php -r "require_once 'config.php'; echo 'DB_HOST: ' . DB_HOST . PHP_EOL;"
```

---

## 🗃️ Database Setup

```sql
-- Create database and table
CREATE DATABASE myapp_db;
USE myapp_db;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Insert sample data
INSERT INTO users (name, email) VALUES 
('John Doe', 'john@example.com'),
('Jane Smith', 'jane@example.com');
```

---

## 🧪 Testing & Verification

### Test Commands:
```bash
# 1. Test configuration
php test.php

# 2. Test API endpoint
curl http://localhost:8000/api/users.php

# 3. Test with POST data
curl -X POST http://localhost:8000/api/users.php \
  -H "Content-Type: application/json" \
  -d '{"name":"John","email":"john@example.com"}'

# 4. Quick config test
php -r "require 'config.php'; echo '✅ Config loaded: ' . APP_NAME;"
```

### Create `test.php`:
```php
<?php
require_once 'config.php';

echo "=== Configuration Test ===\n";
echo "App Name: " . APP_NAME . "\n";
echo "DB Host: " . DB_HOST . "\n";
echo "DB Name: " . DB_NAME . "\n";
echo "Environment: " . APP_ENV . "\n";

// Test DB connection
try {
    $pdo = new PDO("mysql:host=".DB_HOST.";dbname=".DB_NAME, DB_USER, DB_PASS);
    echo "✅ Database: Connected\n";
} catch (PDOException $e) {
    echo "❌ Database: Failed - " . $e->getMessage() . "\n";
}

echo "========================\n";
?>
```

---

## 🚀 Deployment Commands

### Local Development:
```bash
# Start PHP built-in server
php -S localhost:8000

# Test API
curl http://localhost:8000/api/users.php
```

### Production Setup:
```bash
# Set production environment
nano .env
# Change: APP_ENV=production

# Secure .env permissions
chmod 600 .env

# Verify production config
php test.php
```

---

## 🖥️ Editor Cheat Sheet

### Nano (Beginner Friendly):
```bash
nano .env
# Ctrl + O → Save
# Ctrl + X → Exit
# Ctrl + G → Help
```

### Vim (Advanced):
```bash
vim .env
# i → Insert mode
# Esc → Command mode  
# :w → Save
# :q → Quit
# :wq → Save & Quit
# :q! → Quit without saving
```

### VS Code (GUI):
```bash
# If VS Code is installed
code .env

# Or open entire project
code .
```

---

## ⚡ Quick Reference

| Task | Command |
|------|---------|
| Edit .env | `nano .env` |
| Test config | `php test.php` |
| Start server | `php -S localhost:8000` |
| Test API | `curl http://localhost:8000/api/users.php` |
| Install deps | `composer install` |

---

## 🆘 Troubleshooting

### Common Issues:

**Permission Denied:**
```bash
sudo chmod 644 .env
sudo nano .env
```

**Editor Not Found:**
```bash
# Install nano
sudo apt-get install nano

# Or use vi (usually pre-installed)
vi .env
```

**Database Connection Failed:**
```bash
# Check .env values
nano .env
# Verify DB_HOST, DB_NAME, DB_USER, DB_PASS
```

---

<div align="center">

### ⭐ Don't forget to star this repo if you find it useful!

**Start your next PHP project in seconds!** ⚡

</div>
