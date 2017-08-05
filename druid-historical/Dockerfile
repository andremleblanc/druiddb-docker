FROM anapsix/alpine-java
RUN apk update
RUN apk add \
  curl

RUN curl -O http://static.druid.io/artifacts/releases/druid-0.9.2-bin.tar.gz
RUN tar -xzf druid-0.9.2-bin.tar.gz

WORKDIR /druid-0.9.2
RUN bin/init

RUN sed -ri 's/^(\s*)(druid\.zk\.service\.host\s*=\s*localhost\s*$)/\1druid.zk.service.host=zookeeper/' conf-quickstart/druid/_common/common.runtime.properties
RUN sed -ri 's/^(\s*)(druid.metadata.storage.connector.connectURI.*$)/\1druid.metadata.storage.connector.connectURI=jdbc:derby:\/\/derby:1527\/var\/druid\/metadata.db;create=true/' conf-quickstart/druid/_common/common.runtime.properties
RUN sed -ri 's/^(\s*)(druid.extensions.loadList.*$)/\1druid.extensions.loadList=["druid-kafka-indexing-service"]/' conf-quickstart/druid/_common/common.runtime.properties
EXPOSE 8083
CMD java -server -Xms1g -Xmx1g -XX:MaxDirectMemorySize=1280m -Duser.timezone=UTC -Dfile.encoding=UTF-8 -Djava.io.tmpdir=var/tmp -Djava.util.logging.manager=org.apache.logging.log4j.jul.LogManager -cp "conf-quickstart/druid/_common:conf-quickstart/druid/historical:lib/*" io.druid.cli.Main server historical
