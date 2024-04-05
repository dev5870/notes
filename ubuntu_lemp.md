### 1. Install Nginx

```sudo apt update```

```sudo apt install nginx```

### 2. Install MySQL

```sudo apt install mysql-server```

```sudo mysql_secure_installation```

```sudo mysql```

```create database laravel;```

```create user 'user'@'localhost' identified by 'password';```

### 3. Install PHP

```sudo add-apt-repository universe```

```sudo apt install php-fpm php-mysql```

### 4. Create virtual host

#### 4.1 Adding your local domain name to hosts:
```sudo nano /etc/hosts```
```127.0.0.1	x.com```

#### 4.2 Create virtual host:
```sudo nano /etc/nginx/sites-available/x```

> server {
> 
>     listen 80;
> 
>     server_name x.com;
> 
>     root /home/user/workspace/site/public;
> 
>     index index.php;
> 
>     location / {
>         try_files $uri $uri/ /index.php?$args;
>     }
>     location ~ \.php$ {
>         include snippets/fastcgi-php.conf;
>         fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
>     }
> }

```sudo ln /etc/nginx/sites-available/x /etc/nginx/sites-enabled/```

```sudo service nginx restart```

#### 4.3 If get error:
```sudo -u www-data stat /home/user/workspace/site/```

```sudo gpasswd -a www-data user```

### 5. Install composer

```sudo apt install composer```

### 6. Install Laravel

```composer create-project laravel/laravel:^10.0 site```

```sudo apt install php8.1-xml php8.1-curl```

```cp .env.example .env```

```php artisan key:generate```

