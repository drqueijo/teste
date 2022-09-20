Parte 2 docker 1
Parte 2 docker
Created
Class Tecnologias emergentes
Type
Materials
Reviewed
1. É possível trabalharmos com Volumes, onde apontamos os arquivos locais
do nosso computador para o container.
a. Vamos criar uma pasta chamada html
b. Dentro dessa pasta vamos criar o arquivo index.html e adicionar um html
simples dentro dela.
c. Vamos criar nosso container passando o novo parametro de volumes: docker
run -p 8000:80 -v $(pwd)/html:/usr/share/nginx/html nginx
d. Se acessarmos localhost:8000 veremos nosso HTML funcionando.
2. Criando a nossa Receita de Bolo com o Dockerfile
a. Crie um arquivo chamado Dockerfile, dentro dele digite:
i.
FROM nginx:latest
COPY html/index.html /usr/share/nginx/html/
b. Em seguida podemos digitar o comando para executar esse Dockerfile: docker
build -t alexmpereira/unialfa-nginx .
c. Se dermos um docker images, veremos na lista a nossa imagem criada.
d. Agora podemos criar um container a partir da nossa imagem: docker run -p
8000:80 alexmpereira/unialfa-nginx
@August 24, 2022 2:23 PM
Parte 2 docker 2
e. Para subir no docker hub nossa imagem personalizada, digite: docker push
alexmpereira/unialfa-nginx
3. Trabalhando com o docker-compose.yml
a. Crie um arquivo chamado docker-compose.yml
b. Dentro desse arquivo vamos criar as configuracoes:
i.
version: '3'
services:
nginx:
container_name: nginx-unialfa
image: unialfa-nginx
build:
context: .
dockerfile: ./Dockerfile
ports:
- "8000:80"
volumes:
- ./html:/usr/share/nginx/html
c. para subirmos usaremos o comando docker-compose up -d
d. docker-compose é uma ferramenta que usa o docker para conseguir criar
diversos containers ao mesmo tempo, através de um arquivo manifesto.