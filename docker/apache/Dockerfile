FROM php:5.6-apache

# Atualiza as fontes de repositório para usar repositórios alternativos
RUN echo "deb http://archive.debian.org/debian stretch main" > /etc/apt/sources.list && \
    echo "deb http://archive.debian.org/debian-security stretch/updates main" >> /etc/apt/sources.list && \
    apt-get update -o Acquire::Check-Valid-Until=false -o Acquire::Check-Date=false && \
    apt-get install -y \
    zlib1g-dev \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    zip \
    unzip --allow-unauthenticated

# Instala as extensões PHP necessárias, incluindo GD e mysql para o PHP 5.6
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install gd mysql mysqli pdo pdo_mysql zip bcmath sockets

# Ativar mod_ssl e mod_rewrite
RUN a2enmod headers rewrite ssl

# Copiar VHost
COPY vhost.conf /etc/apache2/sites-available/000-default.conf

# Adicionar certificados SSL
COPY ssl/umentor.test.crt /etc/ssl/certs/
COPY ssl/umentor.test.key /etc/ssl/private/

# Instalar Composer compatível
RUN curl -sS https://getcomposer.org/installer | php -- --version=1.10.17 && \
    mv composer.phar /usr/local/bin/composer
