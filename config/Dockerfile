FROM ubuntu:16.04
RUN apt-get update && apt-get install -y curl

RUN apt-get update
RUN apt-get -y install php7.0 mcrypt php7.0-mcrypt php-mbstring php-pear php7.0-dev php7.0-xml

RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN echo "deb http://packages.microsoft.com/ubuntu/16.04/prod xenial main xenial main" > /etc/apt/sources.list.d/mssql-release.list
RUN apt-get update
RUN ACCEPT_EULA=Y apt-get install -y msodbcsql mssql-tools 
RUN apt-get install unixodbc-dev

RUN apt-get install -y libapache2-mod-php7.0 
RUN apt-get install -y apache2

RUN pecl install sqlsrv
RUN pecl install pdo_sqlsrv

RUN apt-get install -y locales \
	&& echo "en_US.UTF-8 UTF-8" > /etc/locale.gen \
	&& locale-gen

RUN echo "extension=/usr/lib/php/20151012/sqlsrv.so" >> /etc/php/7.0/apache2/php.ini
RUN echo "extension=/usr/lib/php/20151012/pdo_sqlsrv.so" >> /etc/php/7.0/apache2/php.ini
RUN echo "extension=/usr/lib/php/20151012/sqlsrv.so" >> /etc/php/7.0/cli/php.ini
RUN echo "extension=/usr/lib/php/20151012/pdo_sqlsrv.so" >> /etc/php/7.0/cli/php.ini

RUN service apache2 restart

RUN a2enmod rewrite

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]