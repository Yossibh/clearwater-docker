FROM yossibh/clearwater-base
MAINTAINER maintainers@projectclearwater.org

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes clearwater-cassandra
RUN sed -e 's/-user cassandra/-user root/g' -i /etc/init.d/cassandra

RUN /etc/init.d/cassandra start && apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes homestead homestead-prov
RUN sed -e 's/\(echo 0 > \/proc\/sys\/kernel\/yama\/ptrace_scope\)/# \1/g' -i /etc/init.d/homestead
RUN echo 'JVM_OPTS="$JVM_OPTS -nodetach"' >> /etc/cassandra/cassandra-env.sh

COPY cassandra.supervisord.conf /etc/supervisor/conf.d/cassandra.conf
COPY homestead.supervisord.conf /etc/supervisor/conf.d/homestead.conf
COPY nginx.supervisord.conf /etc/supervisor/conf.d/nginx.conf

EXPOSE 8888 8889
