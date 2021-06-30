# Steps to Deploy Laravel Docker to Digital Ocean
Based on the guide by Andrew Schmelyun - [Link to Video](https://www.youtube.com/watch?v=G5Nk4VykcUw)

## Server Setup
1. Make a Digital Ocean Droplet and Copy SSH Keys
2. SSH into Server based on IP Address (ex. 64.63.62.62)

```bash
ssh root@64.63.62.62
```

3. Add Non Root User (ex. laravel) and Set Details

```bash
adduser laravel
```

4. Add them to sudo group

```bash
usermod -aG sudo laravel 
```

5. Refresh User and SSH Back In

```bash
exit
ssh root@64.63.62.62 
```

6. Make Home directory (ex. laraveldocker.test) to contain the files

```bash
cd /home
cd laravel
mkdir laraveldocker.test
cd laraveldocker.test
```

7. Install files on Server from Git and Set up SSH

```bash
git clone URL . 
```

## Setting Up the Firewall

8. View all available firewall settings
```bash
sudo ufw app list
```
9. Allow on OpenSSH so we don't get locked out
```bash
sudo ufw allow OpenSSH
```

10. Enable Firewall
```bash
sudo ufw enable
```

11. Check the status
```bash
sudo ufw status
```

## Install Docker
12. All Commands will be from this article

    https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04

13. Update package lists
```bash
sudo apt update
```

14. Install pre requisites
```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

15. Add GPG Key
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

16. Add the Docker repository to APT sources:
```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```

17. Reupdate
```bash
sudo apt update
```
 
18. Set install from the Docker repo instead of the default Ubuntu repo:

```bash
apt-cache policy docker-ce
```

19. Install Docker

```bash
sudo apt install docker-ce
```

20. Check that it’s running properly

```bash
sudo systemctl status docker
 ```


## Install Docker Compose
21. Curl Docker Compose installer

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```


22. Set the correct permissions so that the docker-compose command is executable:

```bash
sudo chmod +x /usr/local/bin/docker-compose
```
 
23. Verify Installation
```bash
docker-compose --version
```

24. Enter folder and start setup

```bash
cd laraveldocker.test
```

25. Create docker group for user and add teh user
```bash
sudo groupadd docker
sudo usermod -aG docker laravel
su laravel
exit
ssh root@64.63.62.62
```

26. Set up seperate dockercompose prod file

```bash
docker compose -f docker-compose.prod.yml up -d --build
```

## Updating .env File and Laravel Setup
27. Update .env file
```bash 
cd src
nano .env and update it
cd ..
```

28. Check all containers are visible

```bash
docker-compose ps 
```

29. Migrate DB and install composer packages

```bash
docker-compose run --rm composer install	
docker-compose run --rm artisan migrate	
```



