# My SQL 설치하기

## 맥에서 mysql 설치하기

> 명령어

```shell
# my sql 설치하기
brew install mysql
```

## My SQL 서비스 시작하기

> 명령어

```shell
brew services start mysql
```

## My SQL 보안 설정하기

> 명령어 
```shell
mysql_secure_installation
```

> 내용들

```shell
Securing the MySQL server deployment.

Connecting to MySQL using a blank password.

VALIDATE PASSWORD COMPONENT can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD component?

Press y|Y for Yes, any other key for No:  No
Please set the password for root here.

New password:

Re-enter new password:
By default, a MySQL installation has an anonymous user,
allowing anyone to log into MySQL without having to have
a user account created for them. This is intended only for
testing, and to make the installation go a bit smoother.
You should remove them before moving into a production
environment.

Remove anonymous users? (Press y|Y for Yes, any other key for No) : Y
Success.


Normally, root should only be allowed to connect from
'localhost'. This ensures that someone cannot guess at
the root password from the network.

Disallow root login remotely? (Press y|Y for Yes, any other key for No) : Y
Success.

By default, MySQL comes with a database named 'test' that
anyone can access. This is also intended only for testing,
and should be removed before moving into a production
environment.


Remove test database and access to it? (Press y|Y for Yes, any other key for No) : Y
 - Dropping test database...
Success.

 - Removing privileges on test database...
Success.

Reloading the privilege tables will ensure that all changes
made so far will take effect immediately.

Reload privilege tables now? (Press y|Y for Yes, any other key for No) : Y
Success.

All done!
```

## My SQL 접속하기

> 명령어

```shell
mysql -uroot
ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: NO)
```
`-p`옵션 없이 그냥 접속할려고 하면 거부 당한다.

```shell
mysql -uroot -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 10
Server version: 8.0.19 Homebrew
```

## My SQL 종료하기
> 명령어

```shell
brew services stop mysql
```