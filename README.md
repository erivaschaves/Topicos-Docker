Como funciona

Docker utilizando o compose, arquivo de configuração com variáveis de ambiente, criando um container nginx 1.18.0 e um container php 7.4.10-fpm ligados através de um link e criando um container mysql 8.0.21.

Configurar o Container Ngnix
Laravel versão 7.3 ou superior


    Exposição de portas

    80 e 443

    Volume (Obs: verificar se na configuração do docker -> drivers compartilhados, as unidades c: e/ou d: estão habilitadas)

    Logs: nginx/logs -> /var/log/nginx

    Virtual Host: nginx/sites -> /etc/nginx/conf.d

    Virtual Host

    Criando do vhost modelo http://api.dev 

Configurar Container Php

    Exposição de portas

    9000

    Volume (Obs: verificar se na configuração do docker -> drivers compartilhados, as unidades c: e/ou d: estão habilitadas)

    Bibliotecas

    Habilitação de bibliotecas do php através de arquivo de configuração. Ex: MBSTRING, GD, MCRYPT, PDO_MYSQL, etc.

Configuração Container Mysql

    Exposição de portas

    3306

    Volume (Obs: verificar se na configuração do docker -> drivers compartilhados, as unidades c: e/ou d: estão habilitadas)

    Aplicação: mysql/data -> /var/lib/mysql

    Configuração para conexão

        MYSQL_DATABASE = default

        MYSQL_USER = default

        MYSQL_PASSWORD = secret

        MYSQL_ROOT_PASSWORD = root

        MYSQL_PORT = 3306

Como utitilizar

    Clone o repositório usando o comando:

    git clone https://github.com/erivaschaves/Topicos-Docker.git

    Entre na pasta Docker-Compose-Nginx-Php-Laravel-Mysql e copie o arquivo env-example para .env.

    cp env-example .env

    Rode seu container:

    docker-compose up -d

    Adicione os domínios no arquivo de hosts do windows.

    127.0.0.1 localhost

    127.0.0.1 api.dev

    Acessar o shell do container:

    winpty docker exec -it nginx bash

    winpty docker exec -it php-fpm bash

    winpty docker exec -it mysql bash

    Instruções iniciais para rodar o Laravel no localhost:

    Acessar a pasta: cd /var/www/html

    Executar comando para criar pasta vendor do laravel: composer install

    Executar comando para criar arquivo de variáveis de ambiente do laravel: cp .env.example .env

    Executar comando para gerar chaves necessarias para rodar o laravel: php artisan key:generate

    Instruções iniciais para rodar o Laravel no api.dev:

    Acessar a pasta api.dev: cd /var/www/html/api.dev

    Executar comando para criar pasta vendor do laravel: composer install

    Executar comando para criar arquivo de variáveis de ambiente do laravel: cp .env.example .env

    Executar comando para gerar chaves necessarias para rodar o laravel: php artisan key:generate

    Abra no navegador

    http://localhost

    http://api.dev

    Acessando o banco de dados dentro do container Mysql

    mysql -u root -p

    
