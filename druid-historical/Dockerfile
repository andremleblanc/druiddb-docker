FROM openjdk:7
RUN apt-get update
RUN apt-get install -y \
curl

RUN curl -O http://static.druid.io/artifacts/releases/druid-0.9.2-bin.tar.gz
RUN tar -xzf druid-0.9.2-bin.tar.gz

WORKDIR /druid-0.9.2
RUN bin/init
CMD java -server -Xms1g -Xmx1g -XX:MaxDirectMemorySize=1280m -Duser.timezone=UTC -Dfile.encoding=UTF-8 -Djava.io.tmpdir=var/tmp -Djava.util.logging.manager=org.apache.logging.log4j.jul.LogManager -cp "conf-quickstart/druid/_common:conf-quickstart/druid/historical:lib/*" io.druid.cli.Main server historical
