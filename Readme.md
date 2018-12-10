# docker-elasticsearch-ik

docker:Elasticsearch+IK-analyzer 

## Useage

ES_JAVA_OPTS: "-Xms1g -Xmx1g -Des.enforce.bootstrap.checks=true -XX:UseAVX=1"
ELASTIC_PASSWORD: "{{ ELASTIC_PASSWORD }}"


可以通过环境变量选项 `-e ES_JAVA_OPTS="-Xms1g -Xmx1g"` 来设置内存限制

`docker run -d --restart=always --name=elasticsearch -p 9200:9200 -p 9300:9300 -e ES_JAVA_OPTS="-Xms1g -Xmx1g -Des.enforce.bootstrap.checks=true -XX:UseAVX=1" -e "http.host=0.0.0.0" -v /data/elasticsearch/data:/usr/share/elasticsearch/data pytool/docker-elasticsearch-ik `

```

docker run --rm \
  --user elasticsearch \
  -p 9200:9200 -p 9300:9300 \
  --name elasticsearch \
  fl.hbz-nrw.de/jprante/elasticsearch-server-extended:6.3.2.0 \
  java \
  -XX:UseAVX=2 \
  -Dfile.encoding=UTF-8 \
  -Djava.awt.headless=true \
  -Dlog4j2.debug=false \
  -Dlog4j2.disable.jmx=true \
  -Dlog4j.shutdownHookEnabled=false \
  -Dio.netty.allocator.type=pooled \
  -Dio.netty.noUnsafe=true \
  -Dio.netty.recycler.maxCapacity=0 \
  -Dio.netty.noKeySetOptimization=true \
  -Djna.nosys=true \
  -Des.path.home="/elasticsearch" \
  -Des.path.conf="/elasticsearch/conf" \
  -Des.distribution.flavor="oss" \
  -Des.distribution.type="tar" \
  --patch-module java.base=/elasticsearch/lib/patch/java.beans \
  --add-exports java.base/java.beans=org.xbib.elasticsearch.log4j \
  --module-path /elasticsearch/lib \
  --module org.xbib.elasticsearch.server/org.elasticsearch.bootstrap.Elasticsearch \
  -Ebootstrap.memory_lock=false \
  -Enetwork.host="0.0.0.0"
  ```

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