---
title: cacti-syslog-docker
date: 2020-06-19 22:41:29
tags: docker 
---
  這篇文章中的東西都是我之前沒使用過的，用了一個禮拜的時間看 cacti 和 syslog，一個禮拜的時間看 docker。
<!--more-->

## 使用套件
  1. [cacti](https://github.com/scline/docker-cacti.git)
  2. [syslog](https://github.com/Cacti/plugin_syslog)
  3. [rsyslog](https://github.com/rsyslog/rsyslog-docker)
  3. [syslog-ng](https://hub.docker.com/r/balabit/syslog-ng/)
  4. [docker](https://www.docker.com/)

## 開發環境
  MacOS High Sierra 10.13.6

## Docker-compose
```
version: '2'
services:

  cacti:
    image: "smcline06/cacti"
    container_name: cacti
    hostname: cacti
    ports:
      - "80:80"
    environment:
      - DB_NAME=cacti_master
      - DB_USER=cactiuser
      - DB_PASS=cactipassword
      - DB_HOST=db
      - DB_PORT=3306
      - DB_ROOT_PASS=rootpassword
      - INITIALIZE_DB=1
      - TZ=Asia/Taipei
    volumes:
      - cacti-data:/cacti
      - cacti-spine:/spine
      - cacti-backups:/backups
      - ./syslog:/cacti/plugins/syslog
    links:
      - db
  
  db:
    image: maria
    container_name: cacti_db
    hostname: db
    ports:
      - "3306:3306"
    command:
      - mysqld
      - --character-set-server=utf8mb4
      - --collation-server=utf8mb4_unicode_ci
      - --max_connections=200
      - --max_heap_table_size=128M
      - --max_allowed_packet=32M
      - --tmp_table_size=128M
      - --join_buffer_size=128M
      - --innodb_buffer_pool_size=1G
      - --innodb_doublewrite=ON
      - --innodb_flush_log_at_timeout=3
      - --innodb_read_io_threads=32
      - --innodb_write_io_threads=16
      - --innodb_buffer_pool_instances=9
      - --innodb_file_format=Barracuda
      - --innodb_large_prefix=1
      - --innodb_io_capacity=5000
      - --innodb_io_capacity_max=10000
    environment:
      - MYSQL_ROOT_PASSWORD=rootpassword
      - TZ=Asia/Taipei
    volumes:
      - cacti-db:/var/lib/mysql

  syslog_ng:
    image: balabit/syslog-ng:3.14.1
    command: "--no-caps"
    ports:
      - "32774:514/udp"
    environment:
      - DB_NAME=cacti_master
      - DB_USER=cactiuser
      - DB_PASS=cactipassword
      - DB_HOST=db
    volumes:
      - ./syslog-ng/syslog-ng.conf:/etc/syslog-ng/syslog-ng.conf

volumes:
  cacti-db:
  cacti-data:
  cacti-spine:
  cacti-backups:
```

## 心得
  我一開始先在一個 container 實驗，將 cacti + rsyslog + mariaDB 通通安裝在裡面，並且成功收到外面機器傳入的 syslog。

但是在使用 docker-compose 時遇到許多問題，首先是 rsyslog 無法將接收到的 syslog 寫入到 DB 的 table 中，因此我改用 syslog_ng 來接受傳入的 syslog。然後在 cacti 使用 syslog 插件時出現錯誤，發現是套件自動產生的 table 格式不對，因此我需要先 build 一個已經有建好 table 的 docker image。

我上面的 Docker-compose 就是使用自己 build 好的 maria image，其他要自行設定的還有 syslog-ng 以及自己下載的 syslog 插件。

