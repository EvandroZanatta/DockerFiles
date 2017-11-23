# LAMP 7.1

Ambiente LAMP para desenvolvimento com PHP 7.1

## Itens instalados

- Apache 2.4
- PHP 7.1
- MySQL 5.7 (root:123456)
- phpMyAdmin

## Recursos extras

- Node.js 8
- MC (Editor)
- Composer
- Git

## Portas abertas

- 80
- 443

## Ambiente de trabalho

- /var/www/html

## SSL

Se você precisar instalar um certificado SSL no seu ambiente, siga esse artigo https://www.digitalocean.com/community/tutorials/how-to-create-a-ssl-certificate-on-apache-for-ubuntu-14-04.

## Criar imagem

Baixe o arquivo _Dockerfile_ e execute no terminal o comando `docker build -t php71 .`

Execute com o comando `docker run -it --name [nome_do_projeto] -p :80 -v [pastalocal]:/var/www/html/ php71`

