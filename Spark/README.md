# Formação Spark com Pyspark

## Introdução

Spark é uma ferramenta de processamento de dados e é extremamente veloz por ser executado em Cluster (rede de computadores que operam visando um objetivo).

Possui alguns componentes:
- Spark SQL
    - Permite leitura de dados com sintaxe SQL
- Spark Streaming
- Mlib (Machine Learning)
- GraphX (Processamento de Grafos)

## RDD e Dataframe

### RDD -  Resilient Distribuited Datasets

- Estrutura básica do Spark de baixo nível
- Dados imutáveis no cluster
- Pode ser persistindo em disco
- Tolerante a falha
- Operações sobre um RDD criam um novo RDD
- Difícil otimização pelo Spark

- Comandos:
    - Criar lista: `numeros = sc.parallelize([1,2,3,4,5])`
    - Listar quantidade específica: `numeros.take(3)`
    - Fazer um top: `numeros.top(3)`
    - Listar tudo: `numeros.collect()`
    - Outros: count, mean, sum, max, min
    - Filtro: `filtro = numeros.filter(lambda filtro: filtro > 2)`
    - Amostra: `amostra = numeros.sample(True, 0.5, 1)`
    - Mapa: `mapa = numeros.map(lambda mapa: mapa * 2)`



### Dataframe

- Semelhante a uma tabela de BD
- Imutável
- Compatível com objetos dataframe do R e Python
- Tipagem correta

- Comandos:
    - Criação: 
    ```python
    from pyspark.sql import SparkSession

    schema = "id INT, nome STRING, idade INT"
    dados = [[1, "Rian", 22], [2, "Raiane", 20]]
    df = spark.createDataFrame(dados, schema)

    df.show()
    ```
    - É possível agrupar chaves de mesmo nome em somente uma e somar a quantidade dessa chave:
    ```python
    from pyspark.sql.functions import sum

    schema2 = "produtos STRING, vendas INT"
    vendas = [["caneta", 20], ["lápis", 40], ["caneta", 30]]
    df2 = spark.createDataFrame(vendas, schema2)
    agrupado = df2.groupBy("produtos").agg(sum("vendas"))

    agrupado.show
    ```

    - Visualizar somente colunas específicas: `df.select("coluna1", coluna2).show()`

    - Adicionar coluna com cálculo:
    ```python
    from pyspark.sql.functions import expr
    # 20% das vendas
    df2.select("produtos", "vendas", expr("vendas * 0.2")).show()
    ```

    - Ver colunas do df: `df.colums`
    
#### Leitura de CSV Local

- Definindo schema manualmente:

    ```py
    from pyspark.sql.types import *

    schema = "id INT, nome STRING, idade INT"
    pessoa = spark.read.csv("caminho.csv", header=False, schema=schema)
    ```

- Definição de schema automática:

    ```py
    from pyspark.sql.types import *

    pessoa_schema = park.read.load("caminho.csv", header=False, format="csv", sep=",", inferSchema=True)
    ```
    
#### Select no CSV com filtro

```py
from pyspark.sql import functions as func

pessoa_schema.select("nome", "total").where(func.col("total") > 30000).show()

clientes.select("Cliente", "Status").where(func.col("Status") == "Platinum" | func.col("Status") == "Gold").show()

pessoa_schema.select("ano").distinct().show()

#count só funciona com groupBy
pessoa_schema.select("ano").groupBy("ano").count().show()
```

- Operadores:
    - e: &, ou: |, not: ~

#### Ações e Transformações

- Importação: `from pyspark.sql import functions as func`
- OrderBy Crescente: `pessoa_schema.orderBy("nome").show()`
- OrderBy Decrescente: `pessoa_schema.orderBy(func.col("nome").desc()).show()`

- GroupBy com agregação: `pessoa_schema.groupBy("sexo").agg(func.sum("total")).show()`
- Filter: `pessoa.schema.filter(func.col("nome") == "Elizabeth").show()`

#### Persistindo os dados

- Exportação: `pessoa_schema.write.format("formato").save("caminho")`
- Importação: `dados = spark.read.format("formato").load("caminho.csv")`


### Spark SQL

- Tabela:
    - Persistente
    - Objeto tabular que reside em um banco de dados
    - Pode ser gerenciado e consultado utilizando SQL
    - Pode-se transformar Dataframe em Tabela
    - Tipos:
        - Gerenciadas: Armazenadas no warehouse do spark, se excluirmos tudo é apagado (dados e metadados)
        - Não Gerenciadas: Externa, Spark apenas gerencia os metadados, se excluir os dados permanecem onde estavam

<br>

- Views: Mesmo conceito do banco de dados relacional
    - Sessão: Visíveis apenas na própria sessão
        - Criação 1: `df.createOrReplaceTempView("nomeView")`
        - Criação 2: `spark.sql("CREATE OR REPLACE TEMP VIEW nomeView AS select * from tabela")`
        - Consulta: `spark.sql("select * from nomeView).show()`
    - Globais: Visíveus em todas as sessões
        - Criação 1: `df.createOrReplaceGlobalTempView("nomeView")`
        - Criação 2: `spark.sql("CREATE OR REPLACE GLOBAL TEMP VIEW nomeView AS select * from tabela")`
        - Consulta: `spark.sql("select * from global_temp.nomeView).show()`
<br>

- Usando SQL:
    - Sintaxe: `spark.sql("comando sql").show()`
- Transformando DF em tabela gerenciada: `nomeDF.write.saveAsTable("nome da tabela")`
    - Se não for criado nenhum banco, é adicionada em *default*
- Transformar tabela gerenciada em DF: `df = spark.sql("select * from tabela")`
- Sobrescrever a tabela gerenciada: `nomeDF.write.mode("overwrite").saveAsTable("nome da tabela")`
- Atualizar tabela com novos registros: `nomeDF.write.mode("append").saveAsTable("nome da tabela")`
- Salvar DF localmente: `DF.write.format("formato").save("caminho")`
- Transformar arquivo local em tabela (não gerenciada): 
    - `DF.write.option("path", "caminho.csv").saveAsTable("Nome tabela")`
- Verificar se a tabela é gerenciada ou não: `spark.sql("show create table nomeTabela").show(truncate=False)`
    - Se aparecer o Location, é não gerenciada
- Ver se todas as tabelas são gerenciadas ou não: `spark.catalog.listTables()`
- Caminho dos bancos de dados fisicos criados é: ~/spark-warehouse/banco.db/tabela

<br>

- Joins:
    - Nas tabelas: `spark.sql("select tab1.coluna, tab2.coluna" from tab2 inner join tab1 on (tab1.idTab2 = tab2.idTab2)").show()`
    - Em DF: `df.join(df2, df.idDF == df2.idDF, "inner").select("coluna1", "coluna2").show()`

<br>

- Terminal somente para spark.sql: Fora do pyspark execute `spark-sql`


### Criando Aplicações

- Pyspark em um arquivo .py com caminho do csv no código

    ```py
    from pyspark.sql import SparkSession
    from pyspark.sql.functions import *

    if __name__ == "__main__":
        spark = SparkSession.builder.appName("Exemplo").getOrCreate()

        df = spark.read.csv("caminho.csv", header="True")
        df.write.format("console").save()

        spark.stop()
    ```
    - No terminal: `spark-submit caminho.py`

- Pyspark em um arquivo .py com caminho do csv como parâmetro:

    ```py
    import sys
    from pyspark.sql import SparkSession
    from pyspark.sql.functions import *

    if __name__ == "__main__":
        spark = SparkSession.builder.appName("Exemplo").getOrCreate()

        df = spark.read.csv(sys.argv[1], header="True")
        df.write.format("console").save()

        spark.stop()
    ```
    - No terminal: `spark-submit aplicativo.py caminho.csv`

- Conversor de formatos de arquivo:
    ```py
    import sys, getopt
    from pyspark.sql import SparkSession

    if __name__ == "__main__":
        spark = SparkSession.builder.appName("Exemplo").getOrCreate()
        opts, args = getopt.getopt(sys.argv[1:], "t:i:o:")
        formato, infile, outdir = "", "", ""

        for opt, arg in opts:
            if opt == "-t":
                formato = arg
            elif opt == "-i":
                infile = arg
            elif opt == "-o":
                outdir = arg
        df = spark.read.csv(infile, header=True)
        df.write.format(formato).save(outdir)

        spark.stop()
    ```
    - `spark-submit aplicativo.py -t json -i caminho.csv -o destino.json`
