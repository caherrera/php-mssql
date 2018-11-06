FROM carlositline/php-mssql:7.2-apache

RUN if [ ! -f "$APACHE_DOCUMENT_ROOT/index.php" ]; then \
    d=`basename $APACHE_DOCUMENT_ROOT`; \
    composer create-project --prefer-dist laravel/laravel `basename $d`; \
fi