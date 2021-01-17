# 安装ElasticSearch

搜索镜像

```text
docker search elasticsearch
```

[https://hub.docker.com/\_/elasticsearch?tab=tags&page=1&ordering=last\_updated](https://hub.docker.com/_/elasticsearch?tab=tags&page=1&ordering=last_updated)

镜像拉取

```text
docker pull elasticsearch:5.6.8
```

运行

```text
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.10.1
```

访问

```text
http://localhost:9200
```

