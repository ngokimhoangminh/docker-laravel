# Part 1: Build and Run

## CREATE A NEW PROJECT TO TEST

Open a terminal from this directory
```bash
cp .env.example .env
docker-compose build
docker-compose up -d

# Access the terminal of the container
docker exec -it laravel_workspace bash

# Create a new Laravel project
composer create-project laravel/laravel .
```
Open a new terminal from this directory
```bash
# demo is the project name
sudo chown -R $USER project/demo
```
Go back to Terminal first, run the following command to fix permissions
```bash
chown -R $USER:www-data storage
chown -R $USER:www-data bootstrap/cache

chmod -R 775 storage
chmod -R 775 bootstrap/cache
```
Test

Access http://localhost:7878 to test

You can access http://localhost:8081 to access phpMyAdmin with the username `root` and password `password`.

# Part 2: Change Database Information:

## RUN EXISTING PROJECTS

Go to the `projects` folder and clone your project here
Open the `.env` file in the projects/{YOUR_PROJECT} directory, change the database parameters as follows:
```dotenv
DB_CONNECTION=mysql
DB_HOST=docker_dbase
DB_PORT=3306
DB_DATABASE=<Your Database Name>
DB_USERNAME=root
DB_PASSWORD=password
```

Edit the `init.sql` file in the `mysql` directory as follows:
```sql
create database <Your Database Name>;
```

```bash
docker-compose restart
```
To execute Laravel commands such as `php artisan migrate`, `composer install`, or `npm install`, use the docker exec command as follows:

```bash
docker exec -it laravel_workspace bash
```