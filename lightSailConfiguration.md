# Configuration of Linux Instance on AWS LightSail 
Instructions for instance based in ubuntu 20.04 

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

Access can be granted by the following command
```
sudo ufw allow <port>/<protocol>
```
To acchieve the basic configuration, the following commands can be used:
```
$ sudo ufw allow 22
$ sudo ufw allow 80
$ sudo ufw allow 443
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

# 3. Setting up Gunicorn

```
$ gunicorn -b localhost:{port} -w {number of workers} {application name}:app
```


```
/home/ubuntu/venvs/backend/bin/python

/home/ubuntu/venvs/backend/bin/gunicorn -b localhost:8080 -w 4 hello:app

/home/ubuntu/venvs/backend/bin/gunicorn
```
