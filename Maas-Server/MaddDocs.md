# Maas Server Setup 

---

## 1. install MAAS

install Maas using --"Snap" :
```shell
sudo snap install --channel=3.5 maas
```
--channel=[current version]

---

## 2. Install and configure Postgres Database Server

install Postgres Database :
```shell
sudo apt install -y postgresql
```

Reboot the system
```shell
sudo reboot
```

Create Database Server user, password and then database.
```shell
sudo -i -u postgres psql -c "CREATE USER \"maas\" WITH ENCRYPTED PASSWORD 'qwerty'"
```
sakib@maas:~$ sudo -i -u postgres psql -c "CREATE USER \"maas\" WITH ENCRYPTED PASSWORD 'qwerty'"
[sudo] password for sakib: 
CREATE ROLE

now create the database for the user ‘maas’, my database name is “maasDB”
```shell
sudo -i -u postgres createdb -O "maas" "maasDB"
```

to varify the installation :

```shell
sakib@maas:~$ sudo -i -u postgres
postgres@maas:~$ psql
psql (16.6 (Ubuntu 16.6-0ubuntu0.24.04.1))
Type "help" for help.

postgres=# \l
                                                   List of databases
   Name    |  Owner   | Encoding | Locale Provider | Collate |  Ctype  | ICU Locale | ICU Rules |   Access privileges   
-----------+----------+----------+-----------------+---------+---------+------------+-----------+-----------------------
 maasDB    | maas     | UTF8     | libc            | C.UTF-8 | C.UTF-8 |            |           |
 postgres  | postgres | UTF8     | libc            | C.UTF-8 | C.UTF-8 |            |           |
 template0 | postgres | UTF8     | libc            | C.UTF-8 | C.UTF-8 |            |           | =c/postgres          +
           |          |          |                 |         |         |            |           | postgres=CTc/postgres
 template1 | postgres | UTF8     | libc            | C.UTF-8 | C.UTF-8 |            |           | =c/postgres          +
           |          |          |                 |         |         |            |           | postgres=CTc/postgres
(4 rows)

postgres=#
```

 maasDB    | maas     | UTF8     | libc            | C.UTF-8 | C.UTF-8 |            |           |
 </br>---is our database


now, edit the configuration of the databse

```shell
sudo nano /etc/postgresql/14/main/pg_hba.conf
```

add below lines at the end of the configuration in the existing configuration of the above file
```shell
host    maasdb    maas    0/0     md5
```
![ScreenShot](SS-01.png)

Use "ctl+O" to save file, and "ctl+X" for exit

---

## 3. Initialize maas 

using the command 
```shell
sudo maas init region+rack --database-uri "postgres://maas:qwerty@localhost/maasDB"
```
```shell
--database-uri "postgres://<username>:<password>@localhost/<DatabaseName>"
```
</br>

![ScreenShot](SS-02.png)

---
