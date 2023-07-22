#Setar a imagem base que vamos utilizar
FROM php:8.2.8-cli

#Setar o diretório onde iremos trabalhar/executar os comandos
WORKDIR /var/www

#Ajustar o timezone do container para nosso horario brasil
RUN ln -sf /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime

#Atualizar os pacotes
RUN apt-get update && \
    apt-get install libzip-dev -y

#Instalar a extension zip para o php
RUN docker-php-ext-install zip

#Instalar o composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \    
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');"

#Instalar o Laravel
RUN php composer.phar create-project laravel/laravel laravel

ENTRYPOINT [ "php","laravel/artisan","serve" ]
CMD [ "--host=0.0.0.0" ]