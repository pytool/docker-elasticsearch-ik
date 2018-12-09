# docker-elasticsearch-ik

docker:Elasticsearch+IK-analyzer 

## Useage

可以通过环境变量选项 `-e ES_JAVA_OPTS="-Xms1g -Xmx1g"` 来设置内存限制

`docker run -d --restart=always -p 9200:9200 -p 9300:9300 -e "http.host=0.0.0.0" -v /data/elasticsearch/data:/usr/share/elasticsearch/data pytool/docker-elasticsearch-ik`

```
docker run -d --name=elasticsearch-ik -p 9200:9200 -v /data/elasticsearch:/usr/share/elasticsearch/data -e "http.host=0.0.0.0" -e "transport.host=127.0.0.1" -e xpack.security.enabled=false pytool/elasticsearch:ik6.4 
```

```yml
path:
  logs: /data/log
  data: /data/data
```
```
docker run -d --name=elasticsearch-ik -p 9200:9200 -v /data/elasticsearch:/usr/share/elasticsearch/data -e "http.host=0.0.0.0" -e "transport.host=127.0.0.1" -e xpack.security.enabled=false pytool/elasticsearch:ik6.4 /elasticsearch/bin/elasticsearch -Des.config=/data/elasticsearch.yml
```

```
docker run -d --name=elasticsearch-ik -p 9200:9200 -v /data/elasticsearch:/usr/share/elasticsearch/data -e "http.host=0.0.0.0" -e "transport.host=127.0.0.1" -e xpack.security.enabled=false pytool/elasticsearch:ik6.4 /elasticsearch/bin/elasticsearch -Des.config=/data/elasticsearch.yml
```

> 注意数据卷挂载目录的写入权限。

---

运行Kibana镜像

```
docker run -ti -p 5601:5601 --link=elasticsearch-ik:elasticsearch --name=kibana docker.elastic.co/kibana/kibana:5.4.1
```