# Git

### Introdução

O Git é o sistema de controle de versão mais utilizado no mundo. Ele é baseado em repositórios que contêm versões de códigos e cópias de cada desenvolvedor. Suas operações possuem alto desempenho, proteção com criptografia e é um projeto de código aberto. O repositório é o local onde o projeto será armazenado, e existem alguns servidores especializados em gerenciá-los, como GitHub e Bitbucket. Neste curso, focamos no GitHub, dada sua popularidade entre os desenvolvedores.

### Comandos Principais

Utilize o modelo abaixo para organizar as informações sobre os comandos principais do Git:

**Sintaxe:** `git COMANDO -OPÇÕES`

- `git init`: Inicializa um repositório, a partir daí o diretório atual será reconhecido como um projeto.

- `git status`: Verifica mudanças no projeto.

- `git add .`: Adiciona alterações antes de serem commitadas.

- `git commit -m "Mensagem"`: Realiza um commit com uma mensagem descritiva das alterações feitas.

- `git branch -M nomeBranch`: Muda o nome da branch do projeto.

- `git remote add origin URL_Repositorio`: Adiciona a origem para a qual o projeto será enviado.

- `git remote -v`: Verifica a origem do projeto.

- `git remote rm origin`: Remove a origem do projeto.

- `git push -u origin nomeBranch`: Envia o projeto para a branch especificada do repositório no GitHub.

- `git pull`: Recebe alterações do projeto do GitHub localmente.

- `git clone URL_Projeto`: Inicia um novo projeto específico do GitHub.

- `git rm arquivo`: Remove um arquivo do monitoramento do Git.

- `git log`: Recebe informações de commits realizados.

- `git mv`: Move e renomeia arquivos.

- `git checkout`: Desfaz alterações de um arquivo.

- `git reset`: Reinicia o projeto para o estado do GitHub.

### Branches

Branches são ramificações para separar e organizar as versões do projeto. Geralmente, ao criar uma nova funcionalidade, é recomendável criar uma nova branch e, depois de pronta, unir ao código principal.

- `git branch`: Visualiza as branches do projeto.

- `git branch nome`: Cria uma nova branch.

- `git branch -d nome`: Deleta uma branch.

- `git checkout -b nome`: Muda para a branch especificada.

**Stashs:**

É um recurso que permite aos desenvolvedores salvar temporariamente as mudanças que estão em progresso, sem ter que fazer um commit.

- `git merge nome`: Une as branches com a Master.

- `git stash list` : Lista todos os stashes disponíveis.

- `git stash apply id` : Recupera o Stash.

- `git stash drop id` : Deleta Stash.

**Tags:**

É uma referência específica a um checkpoint do repositório, geralmente utilizado para marcar versões específicas ou lançamentos importantes.

- `git tag -a nome_da_tag -m "Mensagem descritiva"` : Criar tag.

- `git show` : Mostra tag.

- `git checkout nome_da_tag` : Altera a tag.

- `git push origin nome_da_tag`: Envia tag ao repositório.


### Compartilhamento e Atualização de Repositórios

- `git fetch` : Atualiza as branchs e tags criadas no repositório.

- `git pull` : Atualiza o projeto local para a versão mais atualizada que está no repositório remoto.

- `git push` : Envia atualizações para o repo remoto.

**Submódulos:**

Maneira de possuir dois ou mais projetos em um repositório.
É usado o `git submodule add nome_repo` para adicionar um submódulo.
Para verificar os submódulos é usado o `git submodule`.
E para enviar algo para um submodule é utilizado o `git push --recurse-submodules=on-demand`.


### Análise e Inspeção de Repositórios

O `git show` já foi visto anteriormente, porém não tão a fundo. Ele nos dá várias informações úteis como: Minha branch atual, meus commits (inclusive modificações de arquivos entre cada commit) e informações de tags com `git show nome_tag`.

O `git diff` mostra as diferenças da branch atual local com a remota. Serve também para ver diferenças entre arquivos com `git diff arq1 arq2`.

Por fim, o `git shortlog` mostra um log resumido do projeto, assim, podemos saber quais commits foram enviados e quem enviou.


### Administração de Repositórios

- `git clean` : Verifica e limpa arquivos que não estão sendo trackeados (todos que não usei `git add`).

- `git gc` : Identifica arquivos que não são mais necessários no projeto e deleta.

- `git fsck` : Verifica possíveis corrupções em arquivos (comando de rotina para ver se está tudo nos conformes).

- `git reflog` : Mapea todos meus passos no repositório.

- `git archive --format zip --output master_files.zip master` : Faz a compactação do repositório em .zip.


### Markdown

Assim como o HTML, também é uma linguagem de marcação. Utilizado para adicionar estilos a textos na web. É possível exibir trechos de códigos, links, imagens, entre outros.
Os projetos no GitHub geralmente tem um README.md, ele ajuda bastante na documentação.

**Como criar títulos:**

`# Título grande ## Menor...` (Quanto mais `#` menor o título).

**Ênfase nos textos:**

**Negrito:**`**Texto...**`

*Itálico*: `*Texto...*`

_**Ambos**_: `_**Texto...**_`

**Listas:**
- Não ordenada: `* Texto` ou `- Texto`
1. Ordenada: `1. Texto`

**Imagens:**

Sintaxe: `![Texto Alt](link/caminho da imagem)`

**Links:**

Sintaxe: `[Texto do link](link)`

**Códigos:**

Sintaxe: ` ```Código...``` `