FROM amazonlinux:2023.4.20240416.0

# バージョン指定をしないと2.7より前の脆弱性があるバージョンをインストールしてしまうため指定している（そのうち要らなくなるはず）
COPY --from=composer:2.7 /usr/bin/composer /usr/bin/composer

# 初期設定
RUN \
    yum update -y && \
    yum install -y \
        initscripts \
        zip \
        unzip \
        git \
        vim \
        nginx && \
    yum clean all

# PHP+Mysql設定
RUN \
    yum update -y && \
    yum install -y \
        php8.2 \
        php8.2-fpm \
        php8.2-pdo \
        php8.2-mysqlnd \
        php8.2-mbstring && \
    yum clean all

## 起動設定
RUN mkdir -p /var/run/php-fpm/

# Set entrypoint
ENTRYPOINT /usr/sbin/php-fpm && /usr/sbin/nginx -g "daemon off;"
