---
title: docker 和 docker compose.md
author: 老章 mlpy
date: 2024-12-30 14:10:00 +0800
categories: [AIGC]
tags: [aigc]
render_with_liquid: false
---

# Docker

Docker 是一个开源的容器化平台，它让开发者能够将应用程序与其依赖项打包到一个可移植的容器中。

Docker 主要有两个版本：

1. **Docker CE (Community Edition)**
   - 免费版本
   - 适合个人开发者和小型团队
   - 包含核心 Docker 功能

2. **Docker EE (Enterprise Edition)**
   - 付费版本
   - 面向企业级用户
   - 提供额外的安全、管理和支持功能


## Docker 的核心概念

1. **镜像（Image）**
   - 一个只读的模板，包含创建 Docker 容器的指令
   - 类似于虚拟机的快照
   - 可以从 Docker Hub 下载或自己创建

2. **容器（Container）**
   - 镜像的运行实例
   - 可以启动、停止、删除和暂停
   - 相互隔离且安全

3. **Dockerfile**
   - 用于构建 Docker 镜像的文本文件
   - 包含构建镜像所需的所有命令
   ```dockerfile
   FROM node:14
   WORKDIR /app
   COPY package*.json ./
   RUN npm install
   COPY . .
   EXPOSE 3000
   CMD ["npm", "start"]
   ```

4. **Docker Registry**
   - 用于存储 Docker 镜像的仓库
   - Docker Hub 是最常用的公共仓库

## 常用 Docker 命令

- `docker pull` - 拉取镜像
- `docker build` - 构建镜像
- `docker run` - 运行容器
- `docker ps` - 查看运行中的容器
- `docker stop` - 停止容器
- `docker rm` - 删除容器
- `docker images` - 查看本地镜像

# Docker Compose

Docker Compose 是一个用于定义和运行多容器 Docker 应用程序的工具。

## 主要特点

1. **使用 YAML 文件配置**
   - 在 `docker-compose.yml` 文件中定义服务
   - 可以配置网络、卷、环境变量等

2. **单个命令管理所有服务**
   - `docker-compose up` 启动所有服务
   - `docker-compose down` 停止所有服务

3. **环境隔离**
   - 为项目创建独立的环境
   - 避免端口冲突

## docker-compose.yml 示例

```yaml
version: '3'
services:
  web:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      - db
  db:
    image: mongodb
    volumes:
      - db-data:/data/db

volumes:
  db-data:
```

## Docker Compose 常用命令

- `docker-compose up` - 创建和启动容器
- `docker-compose down` - 停止和删除容器
- `docker-compose ps` - 列出项目中的容器
- `docker-compose logs` - 查看服务日志
- `docker-compose exec` - 在运行的容器中执行命令

## Docker vs Docker Compose

1. **使用场景**
   - Docker：适用于单个容器的管理
   - Docker Compose：适用于多容器应用的管理

2. **配置方式**
   - Docker：使用命令行参数或 Dockerfile
   - Docker Compose：使用 YAML 文件统一配置

3. **复杂度**
   - Docker：适合简单应用
   - Docker Compose：适合复杂的多服务应用

4. **维护性**
   - Docker Compose 配置更容易维护和版本控制
   - 可以轻松复制完整的应用程序环境