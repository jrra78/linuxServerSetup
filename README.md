# 1. Linux Server Setup
Basic tutorial for building and deploying applications in AWS LightSails VPS With Ubuntu Linux

## 1. Security: setting the firewall
UFW (Uncomplicated Fire Wall( is installed but disabled on some linux distributions (i.e. Ubuntu), and you need to enable it before opening any ports on your server. But if anything, you can manually install UFW by running the following command:
### 1.1. Installing UFW
To install UFW use: 
```
$ sudo apt install -y ufw
```
### 1.2 Ports configuration
The basic UFW configuration will require access to the following: 

| port | usage |
|------|----------|
| 22   | ssh  |
| 80   | http |
| 443  | https |
| 3306 | mysql |

Access can be granted by the following command
```
sudo ufw allow <port>/<protocol>
```
To acchieve the basic configuration, the following commands can be used:
```
$ sudo ufw allow 22
$ sudo ufw allow 80
$ sudo ufw allow 443
$ sudo ufw allow 3306
```

### 1.3. Check UFW Status

To verify what is currently blocked or allowed, you may use the verbose parameter when running ufw status, as follows:
```
$ sudo ufw status

```
### 1.4. Enable UFW
To enable UFW on your server, run:
```
$ sudo ufw enable
```
Alternatively
```
$ sudo ufw --force enable
```
### 1.5. Disable UFW
To disable UFW on the server, use the following command:
```
$ sudo ufw disable
```
# 2. Installing dependencies
```
$ sudo apt -y update
$ sudo apt -y upgrade 
$ sudo apt -y autoremove --purge
```

```
$ sudo apt -y install python3 python3-venv python3-dev python3-pip
$ sudo apt -y install supervisor nginx git
```

# 3. Create Virtual Environments
Creation of virtual environments is done by executing the command venv:
```
python3 -m venv /path/to/new/virtual/environment
```

# 4. Upgrade PIP

```
pip install --upgrade pip
```

# 5. Install Scipy
scipy packages cann be install via the command line by entering:
```
python -m pip install numpy scipy matplotlib ipython jupyter pandas sympy nose
```

# 5. MySQL Setup

## 6.1 Basic configuration

Changes some of the less secure default options for things like remote root logins and sample users, by using: 
```
$ sudo mysql_secure_installation
```
Validate your acess to the MySQL prompt:
```
$ sudo mysql
```


```
SELECT user,authentication_string,plugin,host FROM mysql.user;
ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'MyPassword';
FLUSH PRIVILEGES;
quit
```


```
CREATE USER 'appUser'@'localhost' IDENTIFIED BY 'appUser123456@1'
```

## 6.2 Validate MySQL server functioning
```
$ systemctl status mysql.service
```
In case the server is not operational, it can be set as operational with the following command:
```
$ sudo systemctl start mysql
```
Check user access for adminitrative tasks: 
```
$ sudo mysqladmin -p -u root version
```
to access with any other user:
```
mysql -u appUser -p
```
to access as root, the instruction will be as follows:
```
$ sudo mysql -u root -p
```
For remote database setup since MySQL must be able to listen for an external IP address where the server can be reached. To enable this, open up your mysqld.cnf file:
```
s sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```
change  bind-address to the 0.0.0.0 ddress, save changes and restart the server by using:
```
$ sudo systemctl restart mysql
```
Access to mysql and create an admin user: 
```
CREATE USER 'admin'@'%' IDENTIFIED BY 'adminUser@123456';
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
SELECT user,host FROM mysql.user;
```
