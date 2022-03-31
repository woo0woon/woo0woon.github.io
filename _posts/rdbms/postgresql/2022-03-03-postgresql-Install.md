---
title: PostgreSQL - 설치
categories: [RDBMS, PostgreSQL]
tags: [RDBMS, PostgreSQL, Install]
---

## 설치하기

```shell
# Install the repository RPM:
sudo yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm

# Install PostgreSQL:
sudo yum install -y postgresql14-server

# Optionally initialize the database and enable automatic start:
sudo /usr/pgsql-14/bin/postgresql-14-setup initdb
sudo systemctl enable postgresql-14
sudo systemctl start postgresql-14
```

## 비밀번호 설정

```shell
# Set admin password
sudo su - postgres
-bash-4.2$ psql

postgres=# \password postgres
Enter new password:********
Enter it again:********
postgres=# \q
```

## 참조
<https://www.postgresql.org/download/linux/redhat/>{:target="_blank"}
