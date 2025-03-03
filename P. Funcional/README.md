# Programação Funcional

### Definição

Programação funcional é o processo de construir software através de composição de funções puras, evitando compartilhamento de estados, dados mutáveis e efeitos colaterais. É declarativa ao invés de Imperativa.

-Eric Elliot

### Funções de Primeira Classe

- zip: Junta listas e transforma em uma nova lista, tupla ou dicionário
    ```python
    nome = [Rian, Junior, James]
    sobrenome = [Santos, Ferreira, Silva]
    juntos = zip(nome, sobrenome)

    list(juntos) #gera lista
    tuple(juntos) #gera tupla
    dict(juntos) #gera dicionário
    ```

- Dá para manipular funções em variáveis
    ```python
    def dobro(x):
        return x * 2
    def quadrado(x):
        return x ** 2

    d = dobro
    q = quadrado
    ```

### Função de Alta Ordem

- É possível passar função como parâmetro de outra função
    ```python
    def quadrado(x):
        return x ** 2

    def processar(lista, funcao):
        for i in lista:
            print(f'{i} => {funcao(i)}')
    
    processar(range(1, 11), quadrado)
    ```

### Closure

- Modelar funções para usar em variáveis posteriormente
    ```python
    def multiplicar(x):
        def calcular(y):
            return x * y
        return calcular

    dobro = multiplicar(2)
    triplo = multiplicar(3)
    print(dobro(10), triplo(10))
    ```

### Lambda

- Função anônima e há um retorno implícito
- Uso com map:
    ```python
    a = [1, 2, 3]
    dobro = list(map(lambda parametro: parametro * 2, a))

    #====================================================#

    #Exemplo prático em uma tupla de dicionários
    compras = (
        {'quantidade': 2, 'preco': 10},
        {'quantidade': 3, 'preco': 20},
        {'quantidade': 4, 'preco': 30}
    )
    totais = tuple(
        map(
            lambda compra: compra['quantidade'] * compra['preco'], compras
        )
    )
    ```
- Uso com filter (filtrar dados a partir de uma condição)
    ```python
    pessoas = [
        {'nome': 'Junior', 'idade': 17},
        {'nome': 'Rian', 'idade': 16},
        {'nome': 'Bill', 'idade': 24},
        {'nome': 'James', 'idade': 25}
    ]
    menores = filter(lambda p: p['idade'] < 18, pessoas)
    ```
- Uso com reduce (funciona como acumulador)
    ```python
    from functools import reduce
    
    pessoas = [
        {'nome': 'Junior', 'idade': 17},
        {'nome': 'Rian', 'idade': 16},
        {'nome': 'Bill', 'idade': 24},
        {'nome': 'James', 'idade': 25}
    ]
    #abaixo, idades é o acumulador e 0 é a inicialização do acumulador
    soma_idades = reduce(lambda idades, p: idades + p['idade'], pessoas, 0)
    ```

### Recursividade

- Função chamando a si própria
    ```python
    def fatorial(n):
        return n * (fatorial(n-1) if (n - 1 > 1) else 1)

    print(f'10! = {fatorial(10)}')
    ```

### Generator

- Uso do yield para retorno parcial e do next:
    ```python
    def sequecia():
        num = 0
        while True:
            num += 1
            yield num
    print(next(sequencia()))
    print(next(sequencia()))
    print(next(sequencia()))
    ```
