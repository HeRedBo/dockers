# dockers

常用 docker 服务容器封装，为开发环境提供完整的服务支持

## 目前已实现服务（容器）

| 服务名称 | 版本 | 访问地址 | 说明 |
|---------|------|---------|------|
| mysql | 8.0+ | localhost:3306 | 关系型数据库 |
| redis | 6.0.9 | localhost:6379 | 缓存数据库 |
| mongodb | 4.4.2 | localhost:27017 | NoSQL数据库 |
| elasticsearch | 8.2.2 | localhost:9200 | 搜索引擎 |
| kibana | 8.2.2 | localhost:5601 | ES可视化工具 |
| logstash | 8.2.2 | localhost:9600 | 日志收集工具 |
| filebeat | 8.2.2 | - | 日志采集器 |
| kafka | 3.9.1 | localhost:9092 | 消息队列 |
| kafka-ui | latest | localhost:8082 | Kafka可视化工具 |
| etcd | v3.5.11 | localhost:2379 | 分布式键值存储 |
| etcdkeeper | latest | localhost:8080 | etcd可视化工具 |
| apisix | 3.2.0+ | localhost:9080 | API网关 |
| apisix-dashboard | 3.0.1 | localhost:9000 | API网关可视化工具 |
| sail | latest | http://localhost:8108/ui/login | 服务管理平台 |
| jaeger | latest | localhost:16686 | 分布式追踪系统 |
| prometheus | v2.53.0 | localhost:9090 | 监控系统 |
| grafana | 11.2.0 | localhost:3000 | 监控可视化工具 |

> ES 目前已经安装 IK 分词与拼音分词插件

## 快速开始

### 1. 克隆项目到本地
```bash
git clone https://github.com/HeRedBo/dockers
cd dockers
```

### 2. 配置环境变量
```bash
cp .env.example .env
```

可以根据需要修改 `.env` 文件中的配置，包括服务端口、密码等。

### 3. 启动服务

在使用 dockers 之前，请确保你的电脑已经安装好 `Docker Desktop` 并且软件已经正常启动。

#### 启动所有服务
```bash
docker compose up -d
```

#### 启动指定服务
```bash
# 例如：启动 MySQL 和 Redis
docker compose up -d mysql redis

# 例如：启动 Elasticsearch 相关服务
docker compose up -d elasticsearch kibana logstash filebeat
```

> 高版本 Docker Desktop 已经使用 `docker compose` 命令替换旧版 `docker-compose` 命令，请根据自己的实际版本来使用对应命令

## 服务配置说明

### Sail 服务特殊配置
1. **创建数据库**：启动 MySQL 服务后，需要创建 `sail` 数据库
2. **导入数据表**：执行 `sail` 目录下的 `sail.sql` 文件来创建数据表
3. **登录信息**：
   - 访问地址：http://localhost:8108/ui/login
   - 账号：admin
   - 密码：admin123

### 其他服务默认凭据

| 服务名称 | 默认用户名 | 默认密码 | 说明 |
|---------|-----------|---------|------|
| mysql | root | 见 .env 文件 | MYSQL_ROOT_PASSWORD |
| mongodb | admin | admin123 | - |
| elasticsearch | elastic | 见 .env 文件 | ELASTIC_PASSWORD |
| grafana | admin | admin123 | 可在 .env 文件中修改 |

## 目录结构

```
godock/
├── apisix/            # API网关配置
├── apisix-dashboard/  # API网关可视化配置
├── dockprom/          # Prometheus 和 Grafana 配置
├── elastic/           # Elastic 相关配置
├── elasticsearch/     # Elasticsearch 配置
├── es-kibana/         # ES 和 Kibana 配置
├── etcd-demo/         # etcd 演示配置
├── filebeat/          # Filebeat 配置
├── grafana/           # Grafana 配置
├── kafka_demo/        # Kafka 演示配置
├── logstash/          # Logstash 配置
├── mysql/             # MySQL 配置
├── prometheus/        # Prometheus 配置
├── redis/             # Redis 配置
├── sail/              # Sail 服务配置
├── zooker-kafka/      # ZooKeeper 和 Kafka 配置
├── .env.example       # 环境变量示例文件
├── docker-compose.yml # 主服务配置文件
└── README.md          # 项目说明文档
```

## 常见问题

1. **服务启动失败**：检查 Docker Desktop 是否正常运行，以及 `.env` 文件配置是否正确
2. **端口冲突**：如果遇到端口冲突，可以修改 `.env` 文件中的端口配置
3. **数据持久化**：所有服务的数据都已配置持久化到本地目录，确保目录权限正确
4. **Sail 服务无法登录**：确保已创建 `sail` 数据库并导入 `sail.sql` 文件

## 注意事项

- 首次启动服务可能需要较长时间，因为需要拉取镜像
- 请确保主机有足够的内存和磁盘空间
- 生产环境部署时请修改默认密码和相关配置
- 定期备份数据目录以防止数据丢失


