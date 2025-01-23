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

 maasDB    | maas     | UTF8     | libc            | C.UTF-8 | C.UTF-8 |  
 </br>---is our database


now, edit the configuration of the databse

```shell
sudo nano /etc/postgresql/16/main/pg_hba.conf
```

add below lines at the end of the configuration in the existing configuration of the above file
```shell
host    maasdb    maas    0/0     md5
```
![ScreenShot](SS-001.png)

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

```shell
http://<server ip>:5240/MAAS
```  
---is our default url

![ScreenShot](SS-03.png)

</br>
so, we need to create admin to login to the web interface
Using Command:

```shell
sudo maas createadmin
```  
![ScreenShot](SS-04.png)

---

## 4. SSH Setup for user

generate ssh key with the following command: 

```shell
sudo ssh-keygen -t rsa -b 2048 -C "ssh-for-sakib"
```

-t --for type of the key
-b --for bit size
-C --for comment

```shell
sakib@maas:~$ sudo ssh-keygen -t rsa -b 2048 -C "ssh-for-sakib"
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): rsa-maas 
```
rsa-mass is the file name of the ssh key
now copy the public key and upload to the server

![ScreenShot](SS-05.png)

click on import ssh and finish to done the setup

---

