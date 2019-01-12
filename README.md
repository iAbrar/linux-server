# Project: Linux Server Configuration

>You will take a baseline installation of a Linux server and prepare it to host your web applications. You will secure your server from a number of attack vectors, install and configure a database server, and deploy one of your existing web applications onto it.

## Installation and Setup Instructions
### Secure your server:
1. Log in to the server by

`ssh -i ~/.ssh/key.pem ubuntu@18.194.188.135`

2. Update all currently installed packages.
`sudo apt-get update`

`sudo apt-get upgrade`

3. Change the SSH port from 22 to 2200.

`sudo ufw default deny incoming`

`sudo ufw default allow outgoing`

 `sudo ufw allow 2200/tcp`

 `sudo ufw allow www`

 `sudo ufw allow ntp`

 `sudo ufw enable`

### Give grader access:
1. Create a new user account named grader

`sudo adduser grader`

2. Give grader the permission to sudo.

`sudo nano /etc/sudoers.d/grader`

   - Add following line to this file:

        `grader ALL=(ALL:ALL) ALL`

3. Create an SSH key pair for grader using the ssh-keygen tool.
   - Generate a SSH key pair on the local machine:
   
    `ssh-keygen`
   
   - Place the public key on the server that we want to use:
   
    `ssh-copy-id grader@18.194.188.135 -i key_name.pub`

   - Log into remote server as root user and edit the following file and copy public key content inside:
   
    `nano /home/grader/.ssh/authorized_keys`
    
   - Now we can log into the remote server through ssh with the following command:
   
     `ssh grader@18.194.188.135 -p 2200 -i ~/.ssh/LinuxProject`
     
### Prepare to deploy your project:
1.  Configure the local timezone to UTC:

  `sudo dpkg-reconfigure tzdata`
 
   - Hit none above, then UTC.
   
2.  Install and configure Apache to serve a Python mod_wsgi application:
   - Install Apache `sudo apt-get install apache2`
   - Install mod_wsgi `sudo apt-get install python-setuptools libapache2-mod-wsgi`
   - Restart Apache `sudo service apache2 restart`

3. Install and configure PostgreSQL:
   - Install PostgreSQL `sudo apt-get install postgresql`
   - Check if no remote connections are allowed `sudo cat /etc/postgresql/9.3/main/pg_hba.conf`
   - Login as user "postgres" `sudo su - postgres`
   - Get into postgreSQL shell `psql`
   - Create a new database named catalog and create a new user named catalog in postgreSQL shell
     
     `CREATE DATABASE catalog;`
     
     `CREATE USER catalog;`
     
   - Set a password for user catalog
   
    `ALTER ROLE catalog WITH PASSWORD 'your_password';`
   
   - Give user "catalog" permission to "catalog" application database
   
     `GRANT ALL PRIVILEGES ON DATABASE catalog TO catalog;`
   
   - Quit postgreSQL  `\q`
   
   - Exit from user "postgres" `exit`

1. move clone directory to `/var/www/catalog/catalog/`


## Resources I used them:
1. [How To Deploy a Flask Application on an Ubuntu VPS](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps)
2.


