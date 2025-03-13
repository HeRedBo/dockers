# 第一阶段：声明构建参数
ARG STACK_VERSION=8.2.2
# 第二阶段：构建镜像

FROM docker.elastic.co/elasticsearch/elasticsearch:${STACK_VERSION}


# 重新声明 ARG，使其在当前阶段生效
ARG STACK_VERSION
# 安装 IK 分词插件
RUN elasticsearch-plugin install --batch \
    https://release.infinilabs.com/analysis-ik/stable/elasticsearch-analysis-ik-${STACK_VERSION}.zip

# 安装拼音插件（可选）
# RUN elasticsearch-plugin install --batch \
#    https://release.infinilabs.com/analysis-pinyin/stable/elasticsearch-analysis-pinyin-${STACK_VERSION}.zip

# 暴露 Elasticsearch 的端口
EXPOSE 9200 9300