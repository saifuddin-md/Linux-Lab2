# AWS EC2 Deployment Guide – Laravel Employee Management System

## 1. Project Architecture

The Laravel Employee Management System will be deployed directly on an AWS EC2 instance.

**Technology Stack:**

- AWS EC2 – Ubuntu 22.04 LTS
- Nginx – Web Server
- PHP-FPM – PHP Processing
- Laravel – Application Framework
- AWS RDS – MySQL Database

## 2. Step-by-Step Deployment

### Step 1: Launch EC2 Instance

1. Log in to the AWS Management Console.
2. Navigate to EC2 and launch a new instance.
3. Select Ubuntu 22.04 LTS.
4. Configure the security group:
   - TCP 22 – SSH
   - TCP 80 – HTTP
5. Download the key pair (`.pem` file).
6. Obtain your AWS RDS endpoint.

### Step 2: Connect to EC2 Using SSH

Connect to your EC2 instance using the downloaded PEM key.

```bash
chmod 400 your-key.pem

ssh -i your-key.pem ubuntu@YOUR_EC2_PUBLIC_IP
```

### Step 3: Install Nginx, PHP, Composer and Git

Update the Ubuntu packages and install the required software.

```bash
sudo apt update
sudo apt upgrade -y

sudo apt install nginx git composer unzip curl -y
```

Install PHP and the required PHP extensions.

```bash
sudo apt install php-fpm php-cli php-mysql php-xml \
php-mbstring php-curl php-zip php-bcmath -y
```

PHP 8.2 is recommended if supported by your Laravel application. PHP 8.1 is another option mentioned in the original guide.

### Step 4: Prepare Nginx Configuration

Create an Nginx configuration file.

```bash
sudo nano /etc/nginx/sites-available/laravel
```

Configure the Laravel application:

```nginx
server {
    listen 80;
    server_name YOUR_EC2_PUBLIC_IP;

    root /var/www/laravel/public;

    index index.php index.html;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php8.2-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

Enable the configuration:

```bash
sudo ln -s /etc/nginx/sites-available/laravel \
/etc/nginx/sites-enabled/

sudo nginx -t

sudo systemctl restart nginx
```

Adjust the PHP-FPM socket according to your installed PHP version.

### Step 5: Deploy Laravel Application

There are two deployment options.

**Option A: Clone from GitHub**

```bash
cd /var/www

sudo git clone YOUR_GITHUB_REPOSITORY_URL laravel

cd laravel
```

**Option B: Copy Local Project Using SCP**

Run this command from your local machine:

```bash
scp -i your-key.pem -r ./your-laravel-project \
ubuntu@YOUR_EC2_PUBLIC_IP:/var/www/laravel
```

### Step 6: Install Dependencies

Navigate to your Laravel project directory.

```bash
cd /var/www/laravel

composer install --no-dev --optimize-autoloader
```

Create the environment file if it does not exist.

```bash
cp .env.example .env
```

Generate the Laravel application key if required.

```bash
php artisan key:generate
```

### Step 7: Configure Database

Edit the Laravel environment file.

```bash
nano .env
```

Configure the AWS RDS MySQL database details.

```ini
DB_CONNECTION=mysql
DB_HOST=YOUR_RDS_ENDPOINT
DB_PORT=3306
DB_DATABASE=YOUR_DATABASE_NAME
DB_USERNAME=YOUR_DATABASE_USERNAME
DB_PASSWORD=YOUR_DATABASE_PASSWORD
```

Save the file.

**Important:** Allow MySQL port 3306 in the RDS security group, with the EC2 security group as the source.

### Step 8: Run Database Migrations

Execute Laravel migrations.

```bash
php artisan migrate --force
```

### Step 9: Set Permissions

Configure Laravel storage and cache permissions.

```bash
sudo chown -R www-data:www-data storage bootstrap/cache

sudo chmod -R 775 storage bootstrap/cache
```

### Step 10: Restart Services

Restart Nginx and PHP-FPM.

```bash
sudo systemctl restart nginx

sudo systemctl restart php8.2-fpm
```

### Step 11: Visit Your Application

Open your browser and enter your EC2 public IP address.

```text
http://YOUR_EC2_PUBLIC_IP
```

You should now see your Laravel Employee Management System homepage.

## 3. Final Deployment Checklist

- [ ] Launch AWS EC2 instance.
- [ ] Configure Ubuntu 22.04 LTS.
- [ ] Configure EC2 security group.
- [ ] Create AWS RDS MySQL database.
- [ ] Connect to EC2 through SSH.
- [ ] Install Nginx.
- [ ] Install PHP and PHP-FPM.
- [ ] Install Composer and Git.
- [ ] Configure Nginx.
- [ ] Deploy Laravel application.
- [ ] Install Composer dependencies.
- [ ] Configure `.env` database credentials.
- [ ] Run database migrations.
- [ ] Configure Laravel permissions.
- [ ] Restart Nginx and PHP-FPM.
- [ ] Access the application through the EC2 public IP.

## 4. Important Production Recommendations

1. Set `APP_DEBUG=false` in production.
2. Use HTTPS with an SSL certificate.
3. Keep database credentials secure.
4. Restrict SSH access to trusted IP addresses.
5. Keep the RDS database private.
6. Configure regular database backups.
7. Never use `chmod 777` for Laravel permissions.

**Note:** This is a cleaned-up, readable version based on the uploaded screenshot. Some original terminal commands and configuration text were too small to read, so the commands above are reconstructed deployment examples rather than an exact transcription.
