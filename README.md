# Laravel Docker 開發環境

這是一個使用 Docker 容器化的 Laravel 開發環境。包括 MySQL 資料庫、PHP 應用、Nginx Web 伺服器和 Redis 伺服器。

## 前提條件

請確保您的系統已經安裝了 Docker 和 Docker Compose。

- [Docker 安裝](https://docs.docker.com/get-docker/)
- [Docker Compose 安裝](https://docs.docker.com/compose/install/)

## 快速開始

啟動 Docker 容器：

```bash
docker-compose up -d --build
```

## 服務

### MySQL 資料庫（db）

- container：db
- port：33306

### PHP（app）

- container：app

### Nginx 伺服器（nginx）

- container：nginx
- port：80, 443

### Redis 伺服器（redis）

- container：redis
- port：6379
