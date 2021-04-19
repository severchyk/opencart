FROM centos:centos7.9.2009
LABEL maintainer "Severyn Matsiak <severyn.matsiak@gmail.com>"

RUN yum -y update; yum -y install epel-release;  \
    yum -y install httpd wget unzip \
    php php-mysql php-gd php-ldap php-odbc php-pear php-xml php-xmlrpc php-mbstring php-snmp php-soap php-mcrypt curl zlib; \
    yum clean all

RUN wget https://github.com/opencart/opencart/releases/download/2.3.0.2/2.3.0.2-compiled.zip; \
    unzip 2.3.0.2-compiled.zip -d /opencart && rm 2.3.0.2-compiled.zip; \
    mv /opencart/upload/.* /var/www/html; \
    mv /opencart/upload/* /var/www/html; \
    rm -rf /opencart

RUN cp /var/www/html/config-dist.php /var/www/html/config.php; \
    cp /var/www/html/admin/config-dist.php /var/www/html/admin/config.php

RUN sed -i -e '/Listen/s/80/8080/' /etc/httpd/conf/httpd.conf; \
    sed -i -e '/AllowOverride/s/none/All/' /etc/httpd/conf/httpd.conf; \
    sed -i -e '/AllowOverride/s/None/All/' /etc/httpd/conf/httpd.conf; \
    sed -i -e '/@@session.sql_mode/s/MYSQL40//' /var/www/html/install/model/install/install.php; \
    chmod -R 775 /var/www/html && chown -R apache:apache /var/www/html

EXPOSE 8080 8443
ENTRYPOINT ["/usr/sbin/httpd","-D","FOREGROUND"]
