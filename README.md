# MariaDB Setup and Configuration Guide for Windows

This guide explains how to set up MariaDB, create a database, and Create Database User

## 1. Installing MariaDB

Installing MariaDB on Ubntu

```shell
apt update && apt install mariadb-server -y
```

## 2. Securing MariaDB

Open the Command Prompt as Administrator and run the following command to secure your installation:

```shell

mysql_secure_installation
```

Follow the prompts to:
Set a root password.
Remove insecure default users and test databases.
Disable remote root login.

## 3. Setting Up the Database

Open terminal and login to MariaDB:

```bash

mysql -u root -p
```

Enter the root password when prompted.

Create a new database and user:

```sql
CREATE DATABASE student_db;
GRANT ALL PRIVILEGES ON springbackend.* TO 'username'@'localhost' IDENTIFIED BY 'your_password';
```
Replace username and your_password with your desired username and password.

Exit MariaDB:

```sql

EXIT;
```

## 4. You will need Database Credentials to Connect Backend with Database
1. DB_HOST
2. DB_USER
3. DB_PASS
4. DB_PORT
5. DB_NAME

# Steps to Deploy App
Launch the Instance (t2.medium)

## Database layer
1. Run the database container (mariadb) at port 3306:3306 and also attach volume to it
   
   ```bash
   docker run -d -p 3306:3306 -v mariadb_data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=redhat mariadb
   ```
   
2. enter into mariadb
   
   ```bash
   docker exec -it mariadb -uroot -predhat
   ```
3. create database
   
   ```sql
   create databse student_db;
   ```
4. exit

## Backend
1. create dockerfile
2. Create application.properties file and inside the file IP will be IP of database container.
3. PUSH the changes to git
4. Cd to the backend 
5. build image
   ```bash
   docker build -t <tagname> .
   ```
6. run image at port 8080

   ``` bash
   docker run -d -p 8080:8080 <imageName>
   ```

## Frontend
1. Create dockerfile
2. edit .env file and IP will be instance IP
3. Build image
4. Run Image at port 80

## Steps to Deploy Via Docker Compose
1. Create Compose.yml file
2. In the backend folder inside the application.properties file in place of IP write **db**
3. Build and run the container
   ```bash
    docker compose up -d
   ```
4. To remove container
   ```bash
   docker compose down
   ```




