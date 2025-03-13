# 第一阶段：声明构建参数
ARG ELASTIC_VERSION
# 第二阶段：构建镜像

FROM docker.elastic.co/elasticsearch/elasticsearch:${ELASTIC_VERSION}

# 安装 IK 分词插件

RUN echo "https://release.infinilabs.com/analysis-ik/stable/elasticsearch-analysis-ik-${ELASTIC_VERSION}.zip"

# RUN elasticsearch-plugin install --batch \
#     # https://release.infinilabs.com/analysis-ik/stable/elasticsearch-analysis-ik-${STACK_VERSION}.zip
#     https://release.infinilabs.com/analysis-ik/stable/elasticsearch-analysis-ik-8.2.2.zip


# 安装拼音插件（可选）
# RUN elasticsearch-plugin install --batch \
#    https://release.infinilabs.com/analysis-pinyin/stable/elasticsearch-analysis-pinyin-${STACK_VERSION}.zip
# 暴露 Elasticsearch 的端口
EXPOSE 9200 9300