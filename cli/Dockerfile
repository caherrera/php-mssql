FROM php:7.2-cli

ARG BUILD_DATE
ARG VCS_REF

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV PHP_XDEBUG_DEFAULT_ENABLE ${PHP_XDEBUG_DEFAULT_ENABLE:-1}
ENV PHP_XDEBUG_REMOTE_ENABLE ${PHP_XDEBUG_REMOTE_ENABLE:-1}
ENV PHP_XDEBUG_REMOTE_HOST ${PHP_XDEBUG_REMOTE_HOST:-"127.0.0.1"}
ENV PHP_XDEBUG_REMOTE_PORT ${PHP_XDEBUG_REMOTE_PORT:-9000}
ENV PHP_XDEBUG_REMOTE_AUTO_START ${PHP_XDEBUG_REMOTE_AUTO_START:-1}
ENV PHP_XDEBUG_REMOTE_CONNECT_BACK ${PHP_XDEBUG_REMOTE_CONNECT_BACK:-1}
ENV PHP_XDEBUG_IDEKEY ${PHP_XDEBUG_IDEKEY:-docker}
ENV PHP_XDEBUG_PROFILER_ENABLE ${PHP_XDEBUG_PROFILER_ENABLE:-0}
ENV PHP_XDEBUG_PROFILER_OUTPUT_DIR ${PHP_XDEBUG_PROFILER_OUTPUT_DIR:-"/tmp"}

LABEL Maintainer="Carlos <caherrera@gmail.com>" \
      Description="php 7.2 container based on php:7.2-apache with pdo_mssql, xDebug enabled & composer installed." \
      org.label-schema.name="carlositline/php:7.2-apache-mssql" \
      org.label-schema.description="php 7.2 container based on php:7.2-apache-mssql with pdo_mssql xDebug enabled & composer installed." \
      org.label-schema.build-date=$BUILD_DATE \
    #   org.label-schema.vcs-url="https://github.com/caherrera/php-7.2-mssql-xdebug-alpine.git" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.schema-version="1.0.0"

RUN set -ex \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && rm -rf /tmp/* 

# COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug-dev.ini

# ENV LC_ALL es_CL.UTF-8
# ENV LANG es_CL.UTF-8
# ENV LANGUAGE es_CL.UTF-8

ENV DOCUMENT_ROOT /var/www/html
RUN sed -ri -e 's!/var/www/html!${DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf


USER www-data
WORKDIR /var/www/html
EXPOSE 8181
CMD php ./public/artisan serve --host=0.0.0.0 --port=8181


