# Introduction

Simple ansible playbook to install [ghost](https://ghost.org) with mysql 5.7 on Fedora.

## Setup

Install fedora. Create a user called fedora with a password (Kimsufi default setup)

Create hosts inventory file with server ip

```bash
cp hosts.example hosts
```

Create ansible vault with the password for `fedora` user

```bash
ansible-vault create passwords.yml
```

```bash
ansible-playbook -i hosts --ask-vault-pass --extra-vars '@passwords.yml' setup.yml
```

## Manual steps

Setup MySQL password

```bash
# grep 'temporary password' /var/log/mysqld.log
# mysql -uroot -p
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

```bash
su - ghostd
cd /var/www/ghost/
ghost install
```

Letsencrypt setup

```bash
certbot --nginx
```
