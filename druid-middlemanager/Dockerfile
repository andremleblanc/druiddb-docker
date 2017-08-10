FROM openjdk:8-jdk
RUN apt-get update
RUN apt-get install \
  curl

RUN curl -sL https://deb.nodesource.com/setup_8.x
RUN apt-get install -y nodejs

RUN curl -O http://static.druid.io/artifacts/releases/druid-0.9.2-bin.tar.gz
RUN tar -xzf druid-0.9.2-bin.tar.gz

WORKDIR /druid-0.9.2
RUN bin/init

RUN sed -ri 's/^(\s*)(druid\.zk\.service\.host\s*=\s*localhost\s*$)/\1druid.zk.service.host=zookeeper/' conf-quickstart/druid/_common/common.runtime.properties
RUN sed -ri 's/^(\s*)(druid.metadata.storage.connector.connectURI.*$)/\1druid.metadata.storage.connector.connectURI=jdbc:derby:\/\/derby:1527\/var\/druid\/metadata.db;create=true/' conf-quickstart/druid/_common/common.runtime.properties
RUN sed -ri 's/^(\s*)(druid.extensions.loadList.*$)/\1druid.extensions.loadList=["druid-kafka-indexing-service"]/' conf-quickstart/druid/_common/common.runtime.properties
RUN sed -ri 's/^(\s*)(druid.metadata.storage.connector.host.*$)/\1druid.metadata.storage.connector.host=derby/' conf-quickstart/druid/_common/common.runtime.properties

CMD java -server -Xms64m -Xmx64m -Duser.timezone=UTC -Dfile.encoding=UTF-8 -Djava.io.tmpdir=var/tmp -Djava.util.logging.manager=org.apache.logging.log4j.jul.LogManager -cp "conf-quickstart/druid/_common:conf-quickstart/druid/middleManager:lib/*" io.druid.cli.Main server middleManager
