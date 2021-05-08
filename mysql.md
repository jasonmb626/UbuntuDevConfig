# MariaDB (Mysql) using docker, hosted on Fedora 34 instance - Linode Cloud provider

## Create ssh keys for this server
```sh
ssh-keygen -t ed2551
```
or leave off -t ed2551 if you'd prefer to default to rsa

specify output
```
/home/jason/.ssh/linode_id_ed25519
```
enter a passphrase for extra security

## Spin up linode instance
From linode web console, create a Fedora 34 linode.

Option 1, add the ssh key you just generated where it asks
(Copy/paste the contents of /home/jason/.ssh/linode_id_ed25519.pub into text box & save.)

Option 2, copy ssh key to server manually. (Requires root password.)
```sh
ssh-copy-id -i /home/jason/.ssh/linode_id_ed25519.pub root@ip.add.r.x
```

Now log in with your ssh key, (or with your root password.)

Option 3, copy ssh key entry to /root/.ssh/authorized_keys manually.

## Install docker, mariadb client, enable/start docker service
```sh
dnf install moby-engine mariadb
systemctl enable docker
systemctl start docker
```
### Create user, set password, add to groups
```sh
useradd -m jason
passwd jason
usermod -aG wheel,docker jason
```
### Set a strong MySQL root password as an environment variable
```sh
vim /etc/environment
```
populate the data (Use a password generator)
```
MYSQL_ROOT_PASSWORD=xxxxxx
```

Reboot the server
```sh
reboot
```

Frankly this kind of got stuck and I had to use the web console to reboot properly.

## Create a volume to store mysql db files
```sh
docker volume create mysql-data
```

This creates an entry in /var/lib/docker/volumes. tarball this up if you want to move/copy it. (This failed when I tried regular zip)

```sh
cd /var/lib/docker/volumes/mysql-data
tar cvfz mysql-data.tgz *
```

## Run a docker instance MySQL container instance

```sh
docker run -d -p 3306:3306 --mount 'type=volume,src=mysql-data,dst=/var/lib/mysql,volume-driver=local' -e MYSQL_ROOT_PASSWORD=$MYSQL_ROOT_PASSWORD --name mysql-project-1 mysql:latest
```

## Log in to mysql shell from host
it seems you have to specify ip (_not_ localhost and port)
```sh
mysql -h 127.0.0.1 -P 3306 -u root -p
```

## Create database user
```
CREATE USER 'dev'@'%' IDENTIFIED BY '12345';
GRANT ALL PRIVILEGES ON *.* TO 'dev'@'%';
FLUSH PRIVILEGES;
```

## Now connect as 'dev' user
```sh
mysql -h 127.0.0.1 -P 3306 -u dev -p
```
You should also be able to connect from anywhere else. 