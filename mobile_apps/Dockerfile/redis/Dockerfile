# Pull base image.
FROM ubuntu:20.04
RUN apt-get update \
    && apt-get install -y gnupg gosu curl ca-certificates zip unzip git supervisor sqlite3 libcap2-bin build-essential wget \
    && mkdir -p ~/.gnupg \
    && echo "disable-ipv6" >> ~/.gnupg/dirmngr.conf \
    && apt-key adv --homedir ~/.gnupg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys E5267A6C \
    && apt-key adv --homedir ~/.gnupg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C300EE8C \
    && echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu focal main" > /etc/apt/sources.list.d/ppa_ondrej_php.list \
    && apt-get update \
    && cd /tmp \    
    && wget http://download.redis.io/redis-stable.tar.gz \
    && tar xvzf redis-stable.tar.gz \
    && cd redis-stable \
    && make \
    && make install \
    && cp -f src/redis-sentinel /usr/local/bin \
    && mkdir -p /etc/redis \
    && cp -f *.conf /etc/redis \
    && rm -rf /tmp/redis-stable* \
    && sed -i 's/^\(bind .*\)$/# \1/' /etc/redis/redis.conf \
    && sed -i 's/^\(daemonize .*\)$/# \1/' /etc/redis/redis.conf \
    && sed -i 's/^\(dir .*\)$/# \1\ndir \/data/' /etc/redis/redis.conf \
    && sed -i 's/^\(logfile .*\)$/# \1/' /etc/redis/redis.conf

# Define mountable directories.
VOLUME ["/data"]

# Define working directory.
WORKDIR /data

# Expose ports.
EXPOSE 6379

# Define default command.
ENTRYPOINT redis-sentinel /etc/redis/sentinel.conf