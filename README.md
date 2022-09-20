slide 1
slide
Created
Class Tecnologias emergentes
Type
Materials
Reviewed
Comandos básicos com containers
Listar as imagens: docker images
Listar os containers: docker ps
Listar os containers que estao parados: docker ps -a
Baixando uma imagem ubuntu: docker run ubuntu
Nesse caso, diferente do hello-world, ele apenas vai criar o container, mas nao vai
iniciar nada.
Para rodar em modo interativo, acessar esse container: docker run -it ubuntu
Para voltar a acessar o container depois de parado, primeiro digite: docker ps -a
Veja na lista qual é o container e digite: docker start -a -i ID_CONTAINER
Baixando e usando a imagem nginx
1. Vamos executar para baixar o nginx e erguer um container: docker run nginx
a. Ele vai ficar em modo iterativo automaticamente
2. Abra um novo terminal e vamos tentar conectar na página desse container: curl
localhost
@August 24, 2022 2:23 PM
slide 2
a. Nesse ponto teremos um acesso invalido, isso por que o container nao
está expondo a porta 80 para acesso externo.
3. Vamos acessar o container, usando o comando: docker exec -it
NOME_CONTAINER bash
4. Após entrar no container, digitamos o endereco para acessar a página: curl
localhost
a. Nesse caso teremos o retorno do html, isso demonstra que dentro do container
temos acesso.
5. Vamos parar nosso container e rodar um novo comando: docker run -it -p 8000:80
nginx
a. Agora estamos passando o parametro -p, que indica que queremos export a
porta 8000 da nossa máquina, para quando eu digitar cair na porta 80 do
container.
b. Agora é só acessarmos fora do container: curl localhost:8000
6. Vamos editar o arquivo index.html desse nginx.
a. Acesse o container do nginx que criamos, usando o nome que ele criou:
docker exec -it NOME_CONTAINER bash
b. Acesse o seguinte caminho no container: cd /usr/share/nginx/html/
c. Primeiro precisar atualizar o sistema lógico do container para instalarmos o VIM
e editar esse arquivo index.html, basta digitar: apt update
d. Finalizando o update, podemos instalar o vim: apt install vim
e. Agora vamos digitar o comando para abrir um editor de texto no próprio
terminal: vi index.html
f. Digite i para entrar no modo de insert.
g. Usando as setas vá onde queira modificar nos textos e feito as alteracoes
digite ESC, em seguida :wq e um ENTER para salvar as edicoes.
h. Agora vou parar o container e executar novamente, para demonstrar que
perdemos todas as alteracoes feitas no arquivo index.html
slide 3
i. Isso por que toda imagem é imutável, as imagens nao mudam. Por isso
quando criamos o container e editamos e matamos o container em
seguida subimos um novo ele vai subir exatamente como está na
imagem.