FROM yossibh/clearwater-base
MAINTAINER maintainers@projectclearwater.org

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes sprout
RUN sed -e 's/\(echo 0 > \/proc\/sys\/kernel\/yama\/ptrace_scope\)/# \0/g' -i /etc/init.d/sprout

COPY chronos.supervisord.conf /etc/supervisor/conf.d/chronos.conf
COPY memcached.supervisord.conf /etc/supervisor/conf.d/memcached.conf
COPY sprout.supervisord.conf /etc/supervisor/conf.d/sprout.conf

EXPOSE 5052 5054
