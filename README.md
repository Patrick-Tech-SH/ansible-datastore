# Ansible for install Database
## Runbook 
It-creates:
- Python3
- Ansible
- Docker
- docker-compose
- MySQL
- Apache2
- PHP
- phpmyAdmin

## Install ansible and require libraries
```
pip3 install -r ../requirements/python-requirements.txt
```

## Install requirements role
```
ansible-galaxy install -f -n -r requirements/galaxy-role-requirement.yml
```

## If phpmyadmin show code not GUI 
### Run this command 
```
sudo a2enmod proxy_fcgi setenvif
sudo a2enconf php7.0-fpm
sudo service apache2 restart
```
ref. : https://askubuntu.com/questions/861493/phpmyadmin-is-displaying-code-instead-of-page

## If want phpMyadmin to firstpage 
1. go to /etc/apache2/sites-available/
2. create "yourdomain.conf
3. insert this 
```
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName your_domain
    ServerAlias www.your_domain
    DocumentRoot /var/www/phpmyadmin
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
4. Let’s enable the file with the a2ensite tool:
``` 
sudo a2ensite your_domain.conf 
```
5. Disable the default site defined in 000-default.conf
```
sudo a2dissite 000-default.conf
```
6. Next, let’s test for configuration errors
```
sudo apache2ctl configtest
```
   You should receive the following output
```
Output
Syntax OK
```
7. Restart Apache to implement your changes
```
sudo systemctl restart apache2
```
ref. : https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-20-04
