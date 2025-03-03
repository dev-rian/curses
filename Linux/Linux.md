# Linux para Desenvolvedores
Neste curso, vi os principais conceitos e comandos do Sistema Operacional Linux. 
Abaixo estão minhas anotações, que conforme eu ia avançando nas aulas, documentava o que eu estava aprendendo.

### Kernel
O Kernel é o software de maior relevância no Sistema Linux. Ele facilita a comunicação entre as aplicações e o hardware. Sua importância é fundamental para o funcionamento adequado do sistema.

### Diretórios
- **/bin:** Armazena arquivos binários.
- **/boot:** Contém arquivos essenciais para a inicialização do sistema operacional.
- **/dev:** Representa arquivos que correspondem a dispositivos de entrada e saída.
- **/etc:** Contém arquivos de configuração.
- **/home:** Diretórios dos usuários.
- **/tmp:** Armazena arquivos temporários.
- **/usr:** Contém arquivos que podem ser apenas lidos, incluindo instruções de comando do Linux.
- **/var:** Mantém arquivos de log.

### Comandos principais

Nesta seção do curso, foi mostrado como manipular arquivos e diretórios. 
Abaixo vou listar os comandos vistos e suas utilidades:

**Sintaxe:** `COMANDO -PARÂMETROS ARQUIVO/DIRETÓRIO`


`cd` Navega entre diretórios.

`ls` Lista diretórios e arquivos.

`cat` Cria arquivo ou ler conteúdo.

`head` Lê primeiras linhas de um documento.

`touch` Cria arquivo ou modifica data de alteração.

`man` É como um manual dos comandos, sua sintaxe é `man COMANDO`.

`mkdir` Cria um diretório ou mais.

`rm` Remove arquivos e diretórios.

`rmdir` Remove somente diretórios.

`cp` Copia arquivo ou diretório;

`mv` Move e renomeia arquivos e diretórios.

`pwd` Mostra o caminho do diretório atual.

`tail` Filtra partes de um documento.

`grep` Procura palavras em um documento.

`find` Ajuda encontrar um arquivo.

### Gerenciamento de Apps e Pacotes

**Atualização de Repositórios**

`sudo apt-get update`

**Atualização de Pacotes e Aplicativos**

`sudo apt-get upgrade`

**Instalação e Remoção de Aplicativos**

`sudo apt-get install nomeApp`
`sudo apt-get purge nomeApp`

**Remoção de Lixo Desnecessário**

`sudo apt-get autoremove`

### Gerenciamento de Usuários e Grupos

**Criação e Remoção de Usuários**

`adduser` Adiciona usuário ao sistema,  ele fica na pasta **/home**.

`userdel` Remove usuários do sistema.

`usermod` Dependendo do parâmetro, renomeia, bloqueia,  desbloqueia user.

`passwd` Altera senha de um user.

`sudo su` Virar superusuário.

`getent group` Visualiza grupos.

`groupadd` Cria novo grupo.

`groupdel` Deleta grupo.

`usermod -a -G nomeGrupo nomeUser` Adiciona usuário a um grupo.

`gpasswd -d nomeUser nomeGrupo` Remove usuário de um grupo.


### Permissões

O sistema de permissões é uma parte fundamental do modelo de segurança baseado em usuários e grupos no Linux. Um usuário ou grupo pode ter acesso a leitura (**R**ead), Escrita (**W**rite) e Execução (E**X**ecute) a diretórios e arquivos.

As permissões são mostradas, com `ls -lh`, assim: `- rwx rwx rwx` onde o 1° campo diz se é arquivo (-) ou diretório (d), 2°, 3° e 4° as permissões do dono, 5°, 6° e 7° permissões dos grupos e os últimos 3 as permissões dos demais users.

O comando para mudar a permissão de um arq/dir é `chmod permissões arq/dir`, no lugar de *permissões* pode-se usar o modo numérico (modo mais usado) para definir as permissões. 

- 0 ⇒ - - - 
- 1 ⇒ - - x
- 2 ⇒ - w -
- 3 ⇒ - w x
- 4 ⇒ r - -
- 5 ⇒ r - x
- 6 ⇒ r w -
- 7 ⇒ r w x

Exemplo: 
`chmod 744 arq.txt` nesse caso, o dono tem todas as permissões, os grupos e demais users apenas leitura.

### Gerenciamento Básico de Redes

No Linux é possível criar uma série de tarefas que visam configurar, monitorar e solucionar problemas relacionados à conectividade e comunicação em uma rede. 

Teste de conexão de um site/ip `ping site/ip`

Visualizar conexões `netstat -a`

Ver conexões TCP `netstat -at`

Ver conexões UDP `netstat -au`

Ver informações da rede `ifconfig`

Descobrir DNS de um site `nslookup site.com`

Ver as conexões TCP em tempo real `tcpdump :`

Descobrir IP da minha maquina `hostname -I`


### Compactação

**tar:**

Compactar 1 arquivo `tar -czvf arqCompac.tar.gz arq/dir`

Compactar vários `tar -czvf arqCompac.tar.gz arq1 arq2 dir1 dir2`

Descompactar no diretório atual `tar -xzvf arqCompac.tar.gz`

Descompactar em outro dir `tar -xzvf arqCompac.tar.gz -C destino/`
Ver conteúdo do arquivo compactado `tar -tvf arqCompac.tar.gz`

**zip:**

Compactar `zip -r arqCompac.zip dir/`

Descompactar `unzip arqCompac.zip -d destino/`