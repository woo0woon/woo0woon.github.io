---
title: PostgreSQL - 원격 접속 설정
categories: [RDBMS, PostgreSQL]
tag: [PostgreSQL, postgres, Remote Access]
---

### 1. PostgreSQL 설정 파일 변경

```shell
# 수신할 IP 주소 설정 (postgresql.conf)
listen_addresses = '*'

# 인증 환경 설정 (pg_hba.conf)
# TYPE  DATABASE        USER            ADDRESS                 METHOD

host    postgres        all             0.0.0.0/0               reject  # 원격에서 postgres db 접속 차단

host    all             all             0.0.0.0/0               scram-sha-256
```

### 2. PostgreSQL 재시작

```shell
sudo systemctl restart postgresql-14
```

### 3. 방화벽 개방

```shell
# 방화벽에서 5432 포트를 개방
sudo firewall-cmd --permanent --zone=public --add-port=5432/tcp
sudo firewall-cmd --reload
```
