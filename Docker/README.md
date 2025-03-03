# Docker

## Seção 1

### Definição

- Software que reduz a complexidade de setup de aplicações
- Onde configura containers (servidores para aplicações)
- É possível criar ambientes independentes e que funcionam em muitos SO's
- E ainda deixa projetos performáticos
- Dividido em duas versões
    - CE: Community Edition, menor suporte, porém sem suporte.
    - EE: Entreprise Edition, obtem suporte

### Container

- Um pacote de código que pode executar uma ação, tipo rodar uma aplicação Python, Node.js, etc
- Projetos são executados dentro dos containers
- Containers utilizam imagens para rodar, ou seja, são dockers que rodam imagens
- Múltiplos containers podem executar juntos

### Imagem

- É o projeto que será executado pelo container
- Dito isso, programamos uma imagem e executamos via container
- Podemos encontrar imagens em hub.docker.com


### Uso

- Pra executar uma imagem usa-se o comando:
    - Executa e para: `docker run <imagem>` 
    - Continua executando:  `docker run -it <imagem>`
- Ver quais containers estão sendo executados: `docker ps`
- Ver containers que já foram executados: `docker ps -a`
- Rodar em background: `docker run -d <imagem>`
- Rodar o nginx é preciso expor a porta com -p:
    - `docker run -d -p 80:80 nginx`
    - Pra parar:
        - Ver o nome ou id do container com `docker ps`
        - Depois dá um `docker stop <nome ou id>`
- O `docker run` sempre cria um novo container
- Reiniciando container em background: `docker start <nome ou id>`
- Reiniciando container em interação: `docker start -i <nome ou id>`
- Definir nome do container: `docker run -d -p 80:80 --name nginx_app nginx`
- Verificar logs:
    - Histórico: `docker logs <nome ou id>`
    - Histórico e acompanha em tempo real: `docker logs -f <nome ou id>`
- Remover container parado: `docker rm <id ou nome>`
- Remover container executando: `docker rm <id ou nome> -f`


## Seção 2

### Criação de imagem

#### O que é necessário

- Um arquivo Dockerfile em uma pasta que ficará o projeto
- FROM: Imagem base
- WORKDIR: Diretório de aplicação
- EXPOSE: Porta de aplicação
- COPY: Quais arquivos precisam ser copiados
    
#### Exemplo com node

- Na pasta do projeto cria um arquivo chamado Dockerfile
- Dentro desse Dockerfile iremos adicionar:
    - ```js
      FROM node
      WORKDIR /app
      COPY nome.js nome2.js //(arquivo por arquivo)
      COPY . . //(copia todos arquivos do projeto)
      EXPOSE porta
      CMD ["node", "app.js"]
      ```
      
- Rodando a imagem criada:
    - No diretório do projeto, executa: `docker build -t <nome do container>:<tag/versão> .`
    - Ver o id com: `docker image ls`
    - Executar: `docker run -d -p 80:80 --name <nome da imagem> <id ou nome do container>`

      
- Alterando a imagem criada:
    - `docker stop <id ou nome da imagem>`
    - (Altera algo)
    - É preciso um novo build
    - O id vai mudar
    - Executar: `docker run -d -p 80:80 --name nome_diferente <novo id>`
 
- Alterando nome da imagem e tag:
    - `docker tag <id> <nome>:<versão>`

### Camadas das Imagens

- São divididas em camadas (layers)
- Cada instrução no Dockerfile representa uma layer
- Possui cache na hora do build

### Download de Imagens

- Comando: `docker pull <imagem>`
- Ao executar o `docker run <imagem`, vai ser mais rápido porque já está em nossa máquina

### Ajuda com os comandos

- Utiliza-se a flag --help depois de um comando
- Exemplo: `docker run --help`

### Múltiplas aplicações em um container

- Executar:
  ```D
  docker run -d -p porta1 --name nome1 <id>
  docker run -d -p porta3 --name nome2 <id>
  ```
  
### Remoção de imagens

- Container parado: `docker rmi <id>`
- Container em execução: `docker rmi -f <id ou nome:tag>`
- Container não utilizado: `docker system prune`
- Container após a utilização: `docker run --rm <container>`

### Copiar arquivos entre containers

- Usa-se o `docker cp imagem1:/diretorio/arquivo ./diretorio_destino`

### Verificar informações de processamento

- Dados de execução de um container utilizado: `docker top <nome ou id>`
- Inspeção de container: `docker inspect <nome ou id>`
- Processamento: `docker stats`

### Autenticação, Envio e Alteração no Docker Hub

- Criar conta no site
- Login: `docker login`
- Enviar imagens:
    - Cria repositório no Docker Hub
    - `docker build -t <usuario>/<nome da imagem no repositorio> .`
    - `docker push <usuario>/<nome da imagem no repositorio>`
- Usá-la:
    - `docker pull <usuario>/<nome da imagem no repositorio>`
    - `docker run --name <nome> -p <porta> -d <usuario>/<nome da imagem no repositorio>:versao`
- Depois de alterar algo na imagem:
    - `docker build -t <usuario>/<nome da imagem no repositorio>:versão .`
    - `docker push <usuario>/<nome da imagem no repositorio>:versão`
- Logout: `docker logout`


## Seção 3

### Volumes

- Uma forma prática de persistir dados em aplicações e não depender de containers
- Quando o container é removido, perdemos os dados
- Por isso, um diretório do computador será um volume

- Tipos:
    - Anônimos (anonymous): Criado pela flag -v e com nome aleatório
    - Nomeados (named): Com nomes e mais fácil para reutilizar
    - Bind mounts: Salvamento dos dados na máquina sem gerenciamento do Docker

- Anônimos (anonymous):
    - `docker run -v /data`
    - Verificar se o volume foi criado: `docker volume ls`
- Nomeado (nomed):
    - `docker run -v nomedovolume:/data`
- Bind mounts:
    - Fica em um diretório da máquina host
    - `docker run -v /diretorio/data:/data`
 
- Criar volume manualmente: `docker volume create <nome>`
    - Depois só atrelar o container ao volume: `docker run -d -p 80:80 --name <nomecontainer> -v <nomeVolume>:/dados/`
- Inspecionar volume: `docker volume inspect nome>`
- Remover volume: `docker volume rm <nome>`
- Remoção de volumes não utilizados: `docker volume prune`
- Volume somente leitura: `docker run -v volume:/data:ro`

## Seção 4

### Networks no Docker

- Uma forma de gerenciar conexão do Docker com outras plataformas ou entre containers
- Existem alguns drivers de rede, e uma rede facilita a comunicação
- Tipos de conexão:
    -   Externa: API
    -   Com host: Com a máquina que está executando o docker
    -   Entre containers: Utiliza o driver bridge

### Comandos

- Listar redes: `docker network ls`
- Criar redes: `docker network create <nome>`
- Remover redes: `docker network rm <nome>`
- Remover redes não utilizadas: `docker network prune`
- Conectar manualmente a redes: `docker network connect <nome rede> <id container>`
- Desconectar container de uma rede: `docker network disconnect <nome rede> <id container>`
- Inspecionar redes: `docker network inspect <nome>`

### Postman

- Programa para testar API e conexão entre containers
- Download em www.postman.com

### Conexão entre Containers

- Precisa de uma rede: `docker network create rede`
- Conectar os containers na rede:
    - `docker run --name container1 --network rede <nome imagem>`
    - `docker run --name container2 --network rede <nome imagem>`