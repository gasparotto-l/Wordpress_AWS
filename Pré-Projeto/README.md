## Introdução
- Neste projeto realizaremos uma estruturação de uma aplicação Wordpress na AWS, utilizando diversos recursos da aws, como conexões bancos de dados e etc. Porém é essencial que antes de tudo soubermos o como funciona o Wordpress e sua configuração, por isso nessa primeira etapa do vamos fazer isso localmente.

## Requisitos
- Computador Pessoal
- Docker Desktop ou Rancher Desktop
- SO Linux ou VM Linux
- Conexão com a Internet
- Visual Studio Code

## Instalação do Wordpress
- Primeiro no seu terminal linux crie uma pasta para armanazenar a aplicação do wordpress e criar seu container
```bash
mkdir WordPress_Local
cd WordPress_Local/
```
- Agora vamos criar um arquivo docker-compose e configura-lo no VS code. Utilize esse comando:
```bash
code docker-compose.yml
```
- Agora no Visual Studio Code configure o Docker-compose dessa maneira:
```bash
services:

  wordpress:
    image: wordpress
    restart: always
    ports:
      - 8080:80
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: exampleuser
      WORDPRESS_DB_PASSWORD: examplepass
      WORDPRESS_DB_NAME: exampledb
    volumes:
      - wordpress:/var/www/html

  db:
    image: mysql:8.0
    restart: always
    environment:
      MYSQL_DATABASE: exampledb
      MYSQL_USER: exampleuser
      MYSQL_PASSWORD: examplepass
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
    volumes:
      - db:/var/lib/mysql

volumes:
  wordpress:
  db:
  
```
## Containerzação
- Agora de volta no terminal, vamos construir nosso container
```bash
docker compose up -d
```
- Conferimos se tudo correu bem
```bash
docker ps
```
- Por último acesse o site online http://localhost:8080

![image](https://github.com/user-attachments/assets/6f3cc1a9-6aea-4f3a-8850-d938a5eaa392)


- Perfeito, agora que testamos localmente, sabemos como utilizar o wordpress e coloca-lo num container docker.
