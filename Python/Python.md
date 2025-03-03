# Python: do Básico ao Avançado

## Fundamentos

### Tipos Básicos

Python é uma linguagem dinamicamente tipada, ou seja, as variáveis podem mudar de tipo sem nenhuma restrição

- Boolean: Expressão lógica, terá como retorno True ou False
- int: Números inteiros
- float: Números com ponto flutuante
- string: Textos
- Lista: Estrutura com índice nos dados
- Dicionário: Estrutura com chave valor
    - `{'Nome': 'Pedro', 'Idade': '27'}`
- None: Equivalente ao Null ou Undefined de outras linguagens

### Operadores Aritméticos

- Adição: +
- Subtração: -
- Multiplicação: *
- Potenciação: **
- Divisão: /
- Divisão com resultado inteiro: //
- Resto: %

### Operadores Relacionais

- Maior: >
- Maior ou igual: >=
- Menor: <
- Menor ou igual: <=
- Igual: ==
- Diferente: !=

### Operadores de Atribuição

- Recepção: =
- Adição: +=
- Subtração: -=
- Multiplicação: *=
- Potenciação: **=
- Divisão: /=
- Divisão com resultado inteiro: //=
- Resto: %=

### Operadores Lógicos

- or: Pelo menos uma das condições deve ser verdadeira para retornar True
- and: Todas as condições devem ser verdadeiras para retornar True
- ^: or exclusivo, utilizado para comparar dois valores booleanos.
- not: O inverso do resultado da condição

### Operadores Unários

- -*variavel*: Retorna o valor da variável negativo, mas não altera a variável
- +*variavel*: Retorna o valor da variável positivo, mas não altera a variável

### Operadores Ternários

- Usa-se uma variável booleana perto da expressão que for verdadeira.
    - Exemplo:
        ```python
        resultado = True
        print('Hoje o resultado do jogo foi', ('derrota', 'vitória')[resultado])
        #vitória
        ```
- Ou usa o if/else:
    - Exemplo:
      ````python
        resultado = True
        print('Hoje o resultado do jogo foi', ('vitória' if resultado else 'derrota'))
      ````

### Outros Operadores
- Operadores de Identidade: is, is not
- Operadores de Pertinência: in, not in

### Conversão de Tipos

- Usa-se o tipo de dado que queremos antes do valor
    - Exemplo: `int(2 + '5')`

### Números

- Definir casas decimais: `round(valor, n_casas)`

### Strings

- São imutáveis
- Aceitam aspas simples e duplas
- Pode pegar elementos da string como se fosse uma lista
    - s = 'Rian Santos':
        - Retorno de um índice específico `s[x]`
        - Retorno de dos elementos antes do índice  `s[:x]`,  depois `s[x:]` e um intervalo `s[x:y]`
        - Retorno de intervalos definidos: `s[::2]` `s[1::2]`
        - Retorno do inverso da string: `s[::-1]`
- Separar string em uma lista de palavras: `variável.split()`
- Tamanho de uma string: len(variavel)
- Remover elementos de uma string no retorno: `strip()` (por padrão, remove espaços em branco das bordas)

### Listas

- Criar lista: `lista[]`
- Adicionar valor: `lista.append(valor)`
- Remover valor ou índice: `lista.remove(valor ou lista[i])`
- Ver índice de um elemento: `lista.indice(valor)`
- Reverter ordem: `lista.reverse()`
- Retorno de dos elementos antes do índice  `lista[:x]`,  depois `lista[x:]` e um intervalo `lista[x:y]`
- Retorno de intervalos definidos: `lista[::2]` `lista[1::2]`
- Retorno do inverso da string: `lista[::-1]`
- Remover indices de um intervalo: `del lista[1::]`

### Tuplas

- Imutável
- SIntaxe:
    - ``python
      x = tuple()
      x = ('elemento',)
      ``

### Dicionários

- Estrutura chave e valor
- `pessoa = {'nome': 'Rian', 'idade': 22, 'cursos': ['python', 'linux', 'sql']}`
- Retorno das chaves: `chave.keys()`
- Retorno dos valores: `chave.values()`
- Retorno das chaves: `chave.keys()`
- Retorno das chaves + valores: `chave.items()`
- Retorno de valores a partir de itens: `pessoa.get(chave)`
- Adicionar valor a uma chave: `pessoa[chave].append(valor)`
- Ler valor e remover chave: `pessoa.pop(chave)`
- Atualizar e adicionar: `pessoa.update('idade': 23, 'sexo': 'masculino')`
- Remover: `del pessoa[chave]`
- Limpar: `pessoa.clear()`

### Conjuntos

- São imutáveis e não garante ordem de inserção com `append`
- `conjunto = {1, 2, 3, 4}`
- `{1, 2, 3} == {3, 1, 2, 3, 3}`
- União: `c1.union(c2)`
- Interseção: `c1.intersection(c2)`
- Atualizar: `c1.update(c2)`
- Diferença: `c1 - c2`

## Estruturas de Controle

### if, elif e else

- Sintaxe:
    - ```python
      if (condição):
        #estrutura de código caso a condição for True
      
      elif (condição):
        #estrutura de código caso a condição for True
      
      else:
        #estrutura de código caso as condições anteriores forem False
      ```
### while

- Estrutura de repetição condicional
- Sintaxe:
    - ```python
      while (condição):
          #bloco de código
          #enquanto a condição for verdadeira, o código vai ser executado
      ```

### for
- Estrutura de repetição pré-definida
- Sintaxe com range():
    - ```python
      for i in range(inicio, fim, intervalo):
          #bloco de código
      ```
- Sintaxe com listas:
    - ```python
      for i in lista:
          #bloco de código
      ```
- Sintaxe com enumerate():
    - ```python
      for indice, valor in enumerate(lista):
          #bloco de código
      ```
- Percorrer dicionários:
    - ```python
      #percorrer chaves
      for i in dic.keys():
          #bloco de código
      #percorrer valores
      for i in dic.values():
          #bloco de código
      #percorrer chaves e valores
      for i in dic.items():
          #bloco de código
      ```
- break e continue
    - Break: Para o laço de repetição
    - Continue: Interrompe a execução e continua pra próxima

# Manipulação de Arquivos

### Lendo Arquivos e imprimindo

- Utiliza-se o `open()` para abrir o arquivo e o `read()` para ler
    - ```python
      arquivo = open('arquivo.txt')
      dados = arquivo.read()
      for x in dados.splitlines():
          print(*x.split(',' #caracter q deseja ignorar))
      arquivo.close()
    
      #ou
      
      arquivo = open('arquivo.txt')
      for x in arquivo():
          print(*x.split(',', end='')
      arquivo.close()
      ```
      
### Try Finally e With

- Try Finally
    - ```python
      try:
          arquivo = open('arquivo.txt')
          for x in arquivo():
              print(*x.split(',', end='')
      finally:
          #independente de erros no try, o finally será executado
          arquivo.close()
      ```

- With
    - ```python
          with arquivo = open('arquivo.txt') as arquivo:
              for x in arquivo():
                  print(*x.split(',', end='')
          #se o arquivo for aberto no with, ele será fechado automaticamente
      ```

### Escrita de Arquivos

- Utiliza-se a letra w (write) como argumento
    - ```python
          with arquivo = open('arquivo.txt', 'w') as arquivo:
              for x in range(10):
                  print(x, file=arquivo)
          #se o arquivo for aberto no with, ele será fechado automaticamente
      ```

### Leitura com CSV

- ```python
  import csv

  with open(arquivo.csv) as leitura:
      for x in csv.reader(leitura):
          print('Nome: {}, Idade: {}'.format(*x))
  ```

- Lendo CSV de uma URL
    - ```python
      import csv
      from urllib import request

      def ler(url):
          with request.urlopen(url) as arquivo:
              dados = arquivo.read().decode('latin1')
              for x in csv.reader(dados.splitlines()):
                  print(f'Cidade: {x[8]}')
      ler(r'https://www.files.cod3r.com.br/curso-python/desafio-ibge.csv')
      ```


### List Comprehension, Dict Comprehension e Generator

- Sintaxe List:
    - ```python
      # lista = [expressão for i in funcao() condição]
      #sem condição
      quadrados = [i * 2 for i in range(1, 10)]
      
      #com condição
      quadrados = [i * 2 for i in range(1, 10) if i%2 == 0]
      ```
- Sintaxe Dict:
    - ```python
      quadrado = {i: i**2 for i in range(1, 11)}
      ```
- Sintaxe do Generator (ocupa menos memória):
    - ```python
      generator = (i * 2 for i in range(1, 10) if i%2 == 0)
      print(next(generator)) #cada print imprime um valor
      ``` 


## Funções

### Conceitos

- Bloco de código que retorna algo e que pode ser chamado posteriormente
- Uma função em Python é um objeto

### Parâmetros

- Contém parâmetros:
    - Posicionais: `def func(a, b, c)` => `func(1, 2, 3)`
    - Nomeados: `def func(a, b, c)` => `func(c=1, b=3, a=2)`
    - Opcionais: `def func(nome='Não informado')` 
    - Variáveis: 
        - ```python
          def soma_n(*numeros): #parâmetro é uma tupla
              soma = 0
              for x in numeros:
                  soma += n
              return soma
              
          soma(1,2,3,4...n)

          #ou

          def brasileirao(**tabela):
              for posicao, time in tabela.items():
                  print(f'{posicao} - {time}')

          brasileirao(1='Flamengo', 2='Palmeiras', 3=Corinthians)
          ```
- Callable:
    - ```python
      def executar(funcao):
          if callable(funcao):
              funcao()
          else:
              print('Não foi passada uma função!')

      def bom_dia():
          print('Bom dia!')

      executar(bom_dia)

      ```
- Não é interessante usar listas para valores padrão em parâmetros, visto que são mutáveis
    - O uso de tuplas é mais viável:
      ```python
      def fibonacci(sequencia=(0, 1)): #0,1 são valores padrões que sempre estarão na tupla
          return sequencia + (sequencia[-1] + sequencia[-2],) #Cria uma nova tupla para cada return
      ```
### Decorator

- É uma função que envolve outra função para estender ou modificar seu comportamento
- ```python
  def decorator_function(original_function):
    def wrapper_function(*args, **kwargs):
        # Código a ser executado antes da chamada da função original, se necessário
        print("Antes de chamar a função original")

        # Chamar a função original e capturar o retorno, se houver
        result = original_function(*args, **kwargs)

        # Código a ser executado após a chamada da função original, se necessário
        print("Depois de chamar a função original")

        # Retornar o resultado da função original, se necessário
        return result

    # Retornar a função interna wrapper_function
    return wrapper_function

  @decorator_function
  def minha_funcao():
      print("Executando minha função original")

  #Chamando a função deorada
  minha_funcao()

  ```



## Orientação a Objetos

### Conceitos

- Ela permite que você modele objetos do mundo real em seu código, criando classes que têm atributos (variáveis) e métodos (funções)
- Classe funciona como molde
- Objeto é a instanciação da classe
- Pilares:
    - Herança
    - Polimorfismo
    - Encapsulamento
    - Abstração
- Membros:
    - ```python
      class Data:
          pass # Classe sem atributos
      d1 = Data() #Instanciação
      d1.data = '10/10/2001' #Mesmo que a classe não tenha atributos, pode-se criar fora dela

      #Métodos
      class Data:
          def to_str(self):
              return f'{self.data}'
      d1 = Data()
      d1.data = '10/10/2001'
      print(d1.to_str())
      ```
- Método `__str__`:
    - É chamado quando o objeto é usado em uma operação de string, como a função print()
    - É chamado implicitamente quando usa-se a função print() para imprimir um objeto

### Construtores

- São métodos chamados na instanciação da classe
- ```python
  class Data:
      def __init__(self, data):
          self.data = data #Criação do atributo data
  ```

### Herança

- Classes podem herdar comportamentos de outra
- ```python
  class Passaro:
    def __init__(self, nome):
        self.nome = nome
        
    def voar(self):
        print('Voando...')
        
    def emitir_som(self):
        print(f'{self.nome} emitindo som...')

  class Pato(Passaro):
    def __init__(self, nome='Pato'):
        super().__init__(nome)
        
    def voar(self):
        print('Voando...')
        
    def emitir_som(self):
        print(f'{self.nome} emitindo som...\nQuack Quack')
  ```

### Encapsulamento

- O atributo privado vai ter __ antes de seu nome
- Getters e Setters deverão ser criados para acessá-los
- É recomendado o uso da função property() para ter controle sobre a leitura e a escrita desse atributo
- ```python
  class Pessoa:
    def __init__(self, id, nome=None):
        self.__nome = nome
        self.id = id
    
    def get_pessoa(self):
        return self.__nome
        
    def set_pessoa(self, nome):
        self.__nome = nome
    
    nome = property(get_pessoa, set_pessoa)
    
    p1 = Pessoa(1)
    p1.set_pessoa("Rian")
    print(p1.get_pessoa())
  ```
- Métodos privados: Seguem o mesmo padrão dos atributos, começa com __
- Sobrecarga de Operadores:
    - é uma técnica que permite que você defina o comportamento de operadores embutidos, como adição, subtração, multiplicação, divisão, entre outros, para os objetos de suas próprias classes
    - ```python
      class Ponto:
        def __init__(self, x, y):    
            self.x = x
            self.y = y

        def __add__(self, other):
            novo_x = self.x + other.x
            novo_y = self.y + other.y
            return Ponto(novo_x, novo_y)

        def __str__(self):
            return f"{self.x}, {self.y}"

            
### Tratamento de Exceções

- Usado para tratamento de possíveis erros
- ```python
  class Exemplo(Exception):
      pass

  try:
      #bloco de código que eventualmente pode dar erro
  except Exemplo as e:
      print(f'Erro: {str(e)}')
  ```


## Pacotes

### Conceitos

- Se refere a um diretório contendo um conjunto de módulos relacionados
- Pacotes são usados para organizar e estruturar grandes programas Python
- Cada diretório deve ter um arquivo (mesmo que vazio) `__init__.py`
- Um pacote contém módulos e eles podem ser chamados em outros locais do código
    - Usa-se `from nome_pacote import nome_modulo`
    - Depois disso pode usar funções desse módulo
- Dá também pra chamar somente as funções dos módulos:
    - `from nome_pacote.nome_modulo import nome_funcao`
- Existe um padrão de projeto que se chama Façade (Fachada)
    - Pega as funções dos módulo e agrupa em somente um
    - Assim quando precisar usá-los, importa só ele
    - ```python
      from mod1.pac1 import func1
      from mod2.pac1 import func2

      __all__= ['func1', 'func2']
      ```


## Gerenciamento de Pacotes

### PIP

- Usado no terminal
- É recomendado atualizar o PIP
    - `pip3 install --upgrade pip`
- Verificar pacotes instalados:
    - `pip3 list`
- Verificar pacotes desatualizados:
    - `pip3 list --outdated`
    - Caso haja, pra atualizar usa-se:
        - `pip3 install --upgrade nome_pacote`
- Instalação do Django
    - `pip3 install --user Django`
- Congelamento de pacotes (instalação de dependências em algum pacote):
    - `pip3 freeze > requirements.txt`
    - `pip3 install -r requirements.txt`


## Isolamento de Ambientes

- Usa-se quando é necessária a utilização de bibliotecas específicas em determinados projetos
- Na pasta do projeto:
    - Cria a pasta venv: `python -m venv .venv`
    - Ativa o venv: `.venv\Scripts\activate`
    - Instala o request: `pip install --requests==versao`
    - Cria arquivo txt com os pacotes: `pip freeze > requirements.txt`

