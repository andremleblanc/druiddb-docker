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
RUN sed -ri 's/^(\s*)(druid.metadata.storage.connector.host.*$)/\1druid.metadata.storage.connector.host=derby/' conf-quickstart/druid/_common/common.runtime.properties

EXPOSE 8081
CMD java -server -Xms256m -Xmx256m -Duser.timezone=UTC -Dfile.encoding=UTF-8 -Djava.io.tmpdir=var/tmp -Djava.util.logging.manager=org.apache.logging.log4j.jul.LogManager -Dderby.stream.error.file=var/druid/derby.log -cp "conf-quickstart/druid/_common:conf-quickstart/druid/coordinator:lib/*" io.druid.cli.Main server coordinator
