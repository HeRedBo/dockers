<div align="center">

# 🐳 Dockers

[![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/HeRedBo/dockers/pulls)

**常用 Docker 服务容器封装，为开发环境提供完整的服务支持**

</div>

---

## 📋 目录

- [✨ 已集成服务](#-已集成服务)
- [🚀 快速开始](#-快速开始)
- [⚙️ 服务配置说明](#️-服务配置说明)
- [📁 目录结构](#-目录结构)
- [❓ 常见问题](#-常见问题)
- [⚠️ 注意事项](#️-注意事项)

---

## ✨ 已集成服务

### 🗄️ 数据库

| 服务 | 版本 | 访问地址 | 说明 |
|:---:|:---:|:---|:---|
| **MySQL** | 8.0+ | `localhost:3306` | 关系型数据库 |
| **Redis** | 6.0.9 | `localhost:6379` | 缓存数据库 |
| **MongoDB** | 4.4.2 | `localhost:27017` | NoSQL 文档数据库 |
| **etcd** | v3.5.11 | `localhost:2379` | 分布式键值存储 |

### 🔍 搜索与分析

| 服务 | 版本 | 访问地址 | 说明 |
|:---:|:---:|:---|:---|
| **Elasticsearch** | 8.2.2 | `localhost:9200` | 搜索引擎（已安装 IK 分词、拼音分词插件） |
| **Kibana** | 8.2.2 | `localhost:5601` | ES 可视化工具 |
| **Logstash** | 8.2.2 | `localhost:9600` | 日志收集与处理 |
| **Filebeat** | 8.2.2 | - | 轻量级日志采集器 |

### 📨 消息队列

| 服务 | 版本 | 访问地址 | 说明 |
|:---:|:---:|:---|:---|
| **Kafka** | 3.9.1 | `localhost:9092` | 分布式消息队列 |
| **Kafka UI** | latest | `localhost:8082` | Kafka 可视化工具 |

### 🌐 API 网关

| 服务 | 版本 | 访问地址 | 说明 |
|:---:|:---:|:---|:---|
| **APISIX** | 3.2.0+ | `localhost:9080` | 高性能 API 网关 |
| **APISIX Dashboard** | 3.0.1 | `localhost:9000` | API 网关可视化控制台 |

### 📊 监控与可观测性

| 服务 | 版本 | 访问地址 | 说明 |
|:---:|:---:|:---|:---|
| **Prometheus** | v2.53.0 | `localhost:9090` | 监控与告警系统 |
| **Grafana** | 11.2.0 | `localhost:3000` | 监控可视化平台 |
| **Jaeger** | latest | `localhost:16686` | 分布式链路追踪 |

### 🛠️ 工具与平台

| 服务 | 版本 | 访问地址 | 说明 |
|:---:|:---:|:---|:---|
| **etcdkeeper** | latest | `localhost:8080` | etcd 可视化工具 |
| **Sail** | latest | `http://localhost:8108/ui/login` | 服务管理平台 |

## 🚀 快速开始

### 1️⃣ 克隆项目

```bash
git clone https://github.com/HeRedBo/dockers.git
cd dockers
```

### 2️⃣ 配置环境变量

```bash
cp .env.example .env
```

> 💡 可根据需要修改 `.env` 文件中的配置，包括服务端口、密码等。

### 3️⃣ 启动服务

> ⚠️ 使用前请确保已安装并启动 [Docker Desktop](https://www.docker.com/products/docker-desktop/)

#### 启动所有服务

```bash
docker compose up -d
```

#### 启动指定服务

```bash
# 启动 MySQL 和 Redis
docker compose up -d mysql redis

# 启动 Elasticsearch 相关服务
docker compose up -d elasticsearch kibana logstash filebeat
```

> 📝 高版本 Docker Desktop 已使用 `docker compose` 命令替换旧版 `docker-compose`，请根据实际版本使用对应命令。

## ⚙️ 服务配置说明

### 🛳️ Sail 服务特殊配置

Sail 是一个服务管理平台，需要以下初始化步骤：

1. **创建数据库**：启动 MySQL 后，创建名为 `sail` 的数据库
2. **导入数据表**：执行 `sail/sail.sql` 文件创建数据表
3. **登录信息**：
   - 访问地址：http://localhost:8108/ui/login
   - 账号：`admin`
   - 密码：`admin123`

### 🔐 默认登录凭据

| 服务 | 用户名 | 密码 | 配置位置 |
|:---:|:---:|:---:|:---|
| **MySQL** | `root` | 见 `.env` 文件 | `MYSQL_ROOT_PASSWORD` |
| **MongoDB** | `admin` | `admin123` | - |
| **Elasticsearch** | `elastic` | 见 `.env` 文件 | `ELASTIC_PASSWORD` |
| **Grafana** | `admin` | `admin123` | `.env` 文件可修改 |

## 📁 目录结构

```
godock/
├── 🌐 apisix/                 # API 网关配置
├── 📊 apisix-dashboard/       # API 网关可视化配置
├── 📈 dockprom/               # Prometheus + Grafana 配置
├── 🔍 elastic/                # Elastic 相关配置
├── 🔎 elasticsearch/          # Elasticsearch 配置
├── 📊 es-kibana/              # ES + Kibana 配置
├── 🔧 etcd-demo/              # etcd 演示配置
├── 📄 filebeat/               # Filebeat 配置
├── 📊 grafana/                # Grafana 配置
├── 📨 kafka_demo/             # Kafka 演示配置
├── 📄 logstash/               # Logstash 配置
├── 🗄️ mysql/                  # MySQL 配置
├── 📈 prometheus/             # Prometheus 配置
├── 🗄️ redis/                  # Redis 配置
├── 🛳️ sail/                   # Sail 服务配置
├── 📨 zooker-kafka/           # ZooKeeper + Kafka 配置
├── ⚙️ .env.example            # 环境变量示例文件
├── 🐳 docker-compose.yml      # 主服务配置文件
└── 📖 README.md               # 项目说明文档
```

## ❓ 常见问题

| 问题 | 解决方案 |
|:---|:---|
| **服务启动失败** | 检查 Docker Desktop 是否正常运行，以及 `.env` 文件配置是否正确 |
| **端口冲突** | 修改 `.env` 文件中的端口配置，更换为未被占用的端口 |
| **数据持久化** | 所有服务数据已配置持久化到本地目录，确保目录权限正确（`chmod -R 777`） |
| **Sail 无法登录** | 确保已创建 `sail` 数据库并导入 `sail/sail.sql` 文件 |
| **容器无法连接** | 检查防火墙设置，确保所需端口已开放 |

---

## ⚠️ 注意事项

- 🕐 **首次启动**：可能需要较长时间下载镜像，请耐心等待
- 💾 **资源要求**：请确保主机有足够的内存（建议 8GB+）和磁盘空间
- 🔒 **生产环境**：部署前务必修改默认密码和相关安全配置
- 💾 **数据备份**：定期备份数据目录，防止意外数据丢失
- 🔄 **版本升级**：升级服务版本前请先备份数据

---

<div align="center">

**如果觉得项目有帮助，欢迎 ⭐ Star 支持！**

[🐛 提交 Issue](https://github.com/HeRedBo/dockers/issues) · [🤝 贡献代码](https://github.com/HeRedBo/dockers/pulls)

</div>


