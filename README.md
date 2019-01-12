# Project: Linux Server Configuration

>You will take a baseline installation of a Linux server and prepare it to host your web applications. You will secure your server from a number of attack vectors, install and configure a database server, and deploy one of your existing web applications onto it.


## Project Screen Shot(s)
![]()

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


1. move clone directory to `/var/www/catalog/catalog/`

## API Reference


## Technology:
-
-

## Resources I used them:
1.
2.

## Future Checklist:
- [ ] uncompleted
- [x] completed :muscle:

