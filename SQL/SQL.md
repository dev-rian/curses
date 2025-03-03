# SQL Para Análise de Dados


### Introdução

O Sistema Gerenciador de Banco de Dados utilizado durante o curso foi o PostgreSQL usando o pgAdmin.
O curso disponibilizou uma query completa para criação das tabelas e colunas do banco fictício que utilizamos nessa jornada de práticas e aprendizado.

### Comandos Principais

- **Select**:

Sintaxe:
```sql
select coluna_1, coluna_2, coluna_3
from schema_1.tabela_1
```
Comando usado para selecionar colunas de tabelas;
Quando selecionar mais de uma coluna, elas devem ser separadas por
vírgula sem conter vírgula antes do comando FROM;
Pode-se utilizar o asterisco (*) para selecionar todas as colunas da tabela.


- **Distinct**:

Sintaxe:
```sql
select distinct coluna_1, coluna_2, coluna_3
from schema_1.tabela_1
```

Comando usado para remover linhas duplicadas e mostrar apenas linhas distintas.
Muito utilizado na etapa de exploração dos dados
Caso mais de uma coluna seja selecionada, o comando SELECT DISTINCT irá retornar todas as combinações distintas.


- **Where**:

Sintaxe:
```sql
select coluna_1, coluna_2, coluna_3
`from schema_1.tabela_1
where condição_x=true
```
Comando utilizado para filtrar linhas de acordo com uma condição.
No PostgreSQL são utilizadas aspas simples para delimitar strings 
No PostgreSQL as datas são escritas no formato 'YYYY-MM-DD' ou 'YYYYMMDD'


- **Order By**:

Sintaxe:
```sql
select coluna_1, coluna_2, coluna_3
from schema_1.tabela_1
where condição_x=true
order by coluna_1
```
Comando utilizado para ordenar a seleção de acordo com uma regra definida.
Por padrão o comando ordena na ordem crescente. Para mudar para a ordem decrescente usar o comando `DESC`.
No caso de strings a ordenação será seguirá a ordem alfabética


- **Limit**:

Sintaxe: 
```sql
select coluna_1, coluna_2, coluna_3
from schema_1.tabela_1
limit N
```
Comando utilizado para limitar o nº de linhas da consulta.
Muito utilizado na etapa de exploração dos dados.


### Operadores

##### Aritméticos:
- `+` Soma
- `-` Subtração
- `*` Multiplicação
- `/` Divisão
- `||` Concatena strings

##### Comparação:
- `=` Igualdade
- `>` Maior
- `<` Menor
- `>=` Maior ou igual
- `<=` Menor ou igual
- `<>` Diferente

##### Lógicos:
- `AND`: Verifica se duas comparações são simultaneamente verdadeiras
- `OR`: Verifica se uma ou outra comparação é verdadeiras
- `BETWEEN`: Verifica quais valores estão dentro do range definido

  Sintaxe: `where price between 100000 and 200000`
- `NOT`: Negação de uma condição

  Sintaxe: `where price not between 100000 and 200000`
- `IN`: Funciona como multiplos ORs

  Sintaxe: `where brand in ('HONDA', 'TOYOTA')`
- `LIKE` e `ILIKE`: Usado com o coringa %, serve para filtrar strings. (`ILIKE` não possui case sensitive)

  Sintaxe: `where first_name like '%ANA%’`
- `IS NULL`: Busca campos nulos

  Sintaxe: `where population is null`

### Funções Agregadas

Ignoram Células com NULL

- `COUNT()`: Contagens de linhas em uma determinada coluna
- Contagem de itens distintos: `select count(distinct nome_coluna)`
- `SUM()`: Soma de todos os itens da coluna
- `MIN()`: Menor item da coluna
- `MAX()`: Maior item da coluna
- `AVG()`: Média dos itens da coluna

### Group By

Serve para agrupar registros semelhantes de uma coluna
Normalmente utilizado em conjunto com as Funções de agregação

Sintaxe:
```sql
select state, count(distinct city) as numero_cidades
from sales.customers
group by state
```

### Having

Serve para filtrar linhas da seleção por uma coluna agregada ou não agregada. O `WHERE` pode ser usado em conjunto, mas em colunas que não são agregadas.

Sintaxe:

```sql
select state, count()
from sales.customers
where state = 'SP'
group by state
having count() > 100
```

### Joins

Servem para combinar colunas de uma ou mais tabelas
É uma boa prática criar aliases para nomear as tabelas utilizadas

Sintaxe:
```sql
select t1.coluna_1, t1.coluna_1, t2.coluna_1, t2.coluna_2
from schema.tabela_1 as t1
COMANDO join schema.tabela_2 as t2
on condição_de_join
```

- Left Join:
Resultado será toda tabela da esquerda do join + interseção entre as tabelas mencionadas

- Right Join:
Resultado será toda tabela da direita do join + interseção entre as tabelas mencionadas

- Inner Join:
Resultado será a interseção entre as tabelas mencionadas

- Full Join:
Resultado será a junção das tabelas mencionadas (colunas com chave estrangeira não se repetem)


### Unions
Union: Faz a junção das colunas especificadas (não repete linha)
Union All: Faz a junção das colunas especificadas (repete linha)

Sintaxe:
```sql
select coluna_1, coluna_2
from schema_1.tabela_1
union / union all
select coluna_3, coluna_4
from schema_2.tabela_2
```

### Subquerys

Servem para consultar dados de outras consultas.

#### Subquery no WHERE:

Sintaxe:

```sql
select *
from tabela
where coluna = (select coluna from tabela2)
```


##### Subquery com WITH:


Sintaxe:

```sql
with alguma_tabela as (
 select coluna1, coluna2
 from tabela
)
select * from alguma_tabela;
```


#### Subquery no SELECT:

Sintaxe:

`select coluna, (select…from…) as tb from tabela`

Para que as subqueries no WHERE e no SELECT funcionem, elas devem retornar apenas um único valor. Além disso, por questões de legibilidade do código, é aconselhável usar o WITH ao invés de usar subquery no FROM.


### Tratamento de Dados

**Conversão de Unidades**
Operador `::` :

Sintaxe:
`select coluna::tipo`

Exemplos:
`select '2021-10-01'::date - '2021-02-01'::date`

Cast:

Sintaxe:
`select cast(coluna as tipo)`

Exemplo:
`select cast('2021-10-01' as date) - cast('2021-02-01' as date)`


**Tratamento Geral**

Case When:

Sintaxe com exemplo:

```sql
SELECT salario,
CASE
 WHEN salario >= 50000 THEN 'Salário Alto'
 WHEN salario >= 30000 and salario < 5000 THEN 'Salário Médio'
 ELSE 'Salário Baixo'
END AS categoria_salario 
FROM funcionarios
```


Coalesce:

Sintaxe com exemplo:

(Preenche campos nulos com o primeiro valor não nulo de uma sequência de valores.)


```sql
select *,
coalesce(populacao, (select avg(populacao) from regiao)) as populacao_ajustada
from regiao
```

**Tratamento de Texto**

`LOWER()`: é utilizado para transformar todo texto em letras minúsculas.
`UPPER()`: é utilizado para transformar todo texto em letras maiúsculas.
`TRIM()`: é utilizado para remover os espaços das extremidades de um texto.
`REPLACE()`: é utilizado para substituir uma string por outra string.


**Tratamento de Datas**

`INTERVAL`:
É utilizado para somar datas na unidade desejada. Caso a unidade não seja informada, o SQL irá entender que a soma foi feita em dias. Calculando a data de hoje mais 10 unidades (dias, semanas, meses, horas).

```sql
select current_date + 10
select (current_date + interval '10 weeks')::date
select (current_date + interval '10 months')::date
select current_date + interval '10 hours'
```

`DATE_TRUNC`:
É utilizado para truncar uma data no início do período. Calculando quantas visitas ocorreram por mês no site da empresa.

```sql
select data_visita, count(*)
from site
group by data_visita
order by data_visita desc
select
date_trunc('month', data_visita)::date as data_visita_mes,
count(*)
from site
group by data_visita_mes
```


`EXTRACT`:
É utilizado para extrair unidades de uma data/timestamp. Calculando qual é o dia da semana que mais recebe visitas ao site.

```sql
select
extract('dow' from data_visita) as dia_da_semana,
count(*)
from site
group by dia_da_semana
```


Operador `-` e `DATEDIFF`:
O cálculo da diferença entre datas com o operador de subtração (-) retorna valores em dias. Para calcular a diferença entre datas em outra unidade é necessário fazer uma transformação de unidades (ou criar uma função para isso). Calculando a diferença entre hoje e '2018-06-01', em dias, semanas, meses e anos.

```sql
select (current_date - '2018-06-01')
select (current_date - '2018-06-01')/7
select (current_date - '2018-06-01')/30
select (current_date - '2018-06-01')/365
select datediff('weeks', '2018-06-01', current_date)
```


### Funções

 criação de funções em SQL permite aos desenvolvedores definir operações personalizadas reutilizáveis em consultas, facilitando a organização do código.

Sintaxe:
```sql
CREATE FUNCTION nome_da_funcao(argumentos)
RETURNS tipo_retorno AS
$$
DECLARE
    --Declaração de variáveis locais
BEGIN
    --Corpo da função (lógica)
    --Retornar um valor usando RETURN*
END;
$$
```


### Manipulação de Tabelas

**Criação de tabela a partir de uma query**

Sintaxe:
```sql
SELECT coluna_1, coluna_2, ..., coluna_n
INTO novo_schema.novo_nome_da_tabela
FROM nome_da_tabela_existente
WHERE condições_opcionais;
```

**Criação de tabela a partir do zero**

Sintaxe:
```sql
CREATE TABLE nome_da_tabela (
    coluna_1 tipo_de_dado_1,
    coluna_2 tipo_de_dado_2
);

INSERT INTO nome_da_tabela (coluna_1, coluna_2, ..., coluna_n)
VALUES(valor_coluna_1, valor_coluna_2, ..., valor_coluna_n);
```

**Exclusão de tabela**

Sintaxe:
`DROP TABLE nome_da_tabela;`

**Atualização de tabela**

Sintaxe:
```sql
UPDATE nome_da_tabela
SET coluna_1 = novo_valor_1, coluna_2 = novo_valor_2, ..., coluna_n = novo_valor_n
WHERE condição;
```

**Deletar linhas da tabela**

Sintaxe:
```sql
DELETE FROM nome_da_tabela
WHERE condição;
```

**Qualquer modificação nas colunas**

Sintaxe:
`ALTER TABLE nome_da_tabela;`

**Adicionar colunas**

Sintaxe:
```sql
ALTER TABLE nome_da_tabela
ADD nome_da_nova_coluna tipo_de_dado;
```

**Mudar o tipo de unidade de uma coluna**

Sintaxe:
```sql
ALTER TABLE nome_da_tabela
ALTER COLUMN nome_da_coluna_existente TYPE novo_tipo_de_dado;
```

**Renomear coluna**

Sintaxe:
```sql
ALTER TABLE nome_da_tabela
RENAME COLUMN nome_da_coluna_existente TO novo_nome_da_coluna;
```

**Deletar coluna**

Sintaxe:
```sql
ALTER TABLE nome_da_tabela
DROP COLUMN nome_da_coluna_existente;
```