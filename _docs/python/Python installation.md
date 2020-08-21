---                  
order: 9            
title: (Python) Python installation   
category: Python                  
---   
   
### yum   
yum groupinstall "Development tools"   
yum -y install net-tools   
yum -y remove mysql-libs    
yum -y install wget   
yum update   
   
### Python   
# 1. python install by yum   
yum install python3   
   
- check   
python3 -V   
   
# 2. pip install by yum   
pip install   
yum install python3-pip   
yum install nano   
   
- check   
pip3 -V   
   
# 3. virtualenv install by yum   
pip3 install virtualenv   
   
- check   
virtualenv --version   
   
   
### Django   
# 1. Install django   
mkdir django-apps   
cd django-apps   
   
# 2. Call env   
virtualenv env   
   
# 3. Activate the virtual environment   
/home/django-apps   
. env/bin/activate   
   
the prefix is changed to env like it below   
(env) [root@localhost django-apps]#   
   
# 4. install the Django package using pip   
pip install django   
   
- version check   
django-admin --version   
   
# 5. Create a Django project   
cd django-apps   
django-admin startproject crypto   
   
# 6. view manage.py   
less manage.py   
   
# 7. info   
__init__.py acts as the entry point for your Python project.   
settings.py describes the configuration of your Django installation and lets Django know which settings are available.   
urls.py contains a urlpatterns list, that routes and maps URLs to their views.   
wsgi.py contains the configuration for the Web Server Gateway Interface. The Web Server Gateway Interface (WSGI) is the Python platform standard for the deployment of web servers and applications.   
   
# 8. setting ip address   
   
vi /home/django-apps/crypto/crypto/settings.py   
ALLOWED_HOSTS = [] ----> ALLOWED_HOSTS = ['192.168.5.187']   
   
# 9. start   
cd /home/django-apps/crypto   
python3 manage.py runserver 192.168.5.187:80   
   
   
error->   
SQLite 3.8.3 or later is required   
solution->   
   
wget https://www.sqlite.org/2018/sqlite-autoconf-3240000.tar.gz   
tar zxvf sqlite-autoconf-3240000.tar.gz   
./configure --prefix=/usr/local   
make   
make install   
export LD_LIBRARY_PATH="/usr/local/lib"   
sqlite3 --version   
   
## How to start   
# 1. Activate the virtual environment   
/home/django-apps   
. env/bin/activate   
   
# 2. sqllite3   
export LD_LIBRARY_PATH="/usr/local/lib"   
   
# 3. cd /home/django-apps/crypto   
python3 manage.py runserver 192.168.5.187:80   
   
--Aapache install   
yum install httpd   
yum install mod_wsgi   
   
--Mysql install   
yum install mysql   
pip3 install pymysql   
