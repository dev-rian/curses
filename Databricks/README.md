# 📌 Databricks: Conceitos e Utilidades

## 🔹 O que é o Databricks?
Databricks é uma plataforma unificada de análise de dados baseada em Apache Spark, projetada para processamento massivo de dados, machine learning e análise avançada. Ele combina Data Engineering, Data Science e BI em um único ambiente escalável e colaborativo.

## 🔹 Principais Conceitos

### 1️⃣ **Lakehouse Architecture**
- Combina os benefícios do **Data Lake** e do **Data Warehouse**.
- Permite armazenar dados brutos, processados e refinados no mesmo local.
- Usa **Delta Lake** para versionamento e otimização dos dados.

### 2️⃣ **Delta Lake**
- Camada de armazenamento que melhora a confiabilidade dos Data Lakes.
- Oferece **ACID Transactions**, **Time Travel** e **Schema Evolution**.
- Otimiza consultas com **Z-Ordering** e **Compaction**.

### 3️⃣ **Clusters**
- Ambiente de computação escalável baseado no Apache Spark.
- Pode ser configurado como **All-Purpose Clusters** (interativo) ou **Job Clusters** (automatizado).
- Suporte a instâncias **Auto-Scaling** para otimização de custo.

### 4️⃣ **Notebooks**
- Interface colaborativa para desenvolvimento em **Python, SQL, Scala e R**.
- Suporta **visualizações interativas** e integração com bibliotecas externas.

### 5️⃣ **Workflows e Jobs**
- Automação de pipelines de ETL e Machine Learning.
- Orquestração de tarefas com **Triggers e Dependências**.

### 6️⃣ **MLflow**
- Gerenciamento completo do ciclo de vida de Machine Learning.
- Rastreia experimentos, registra modelos e facilita a implantação.

### 7️⃣ **Unity Catalog**
- Gerenciamento centralizado de governança e segurança de dados.
- Permite **controle de acessos e auditoria**.

## 🔹 Utilidades e Casos de Uso
✅ **Data Engineering** – ETL massivo, processamento de Big Data.  
✅ **Data Science & Machine Learning** – Treinamento e implantação de modelos.  
✅ **Business Intelligence** – Análises avançadas e geração de insights.  
✅ **Streaming de Dados** – Processamento de dados em tempo real com Spark Streaming.  
✅ **Governança e Segurança** – Controle de acessos e conformidade com regulamentações.  

## 🔹 Prática

### Barra lateral

* **Workspace**: Posso criar notebooks nos Clusters
* **Catalog**: Posso criar tabelas a partir de arquivos
* **Compute**: Onde gerencio meus Clusters

### Formato Parquet

* Otimiza consultas
* Armazena em forma de colunas
* Suporta compressão
* Arquivo dividido em dados e metadados

### Códigos úteis

#### Arquivos gerais

**Criando DF a partir de uma tabela carregada em Catalog**:

```py
%python
df_vinhos = spark.table("vinhos")
```

**Carregando um arquivo para um dataframe**:

```py
%python 
df = spark.read.format('csv').options(header='true', inferSchema='true', delimiter=';').load('/FileStore/tables/carga/clientes_cartao.csv')
```
ou
```py
%python 
df = spark.read.load("caminho.csv", header=False, format="csv", sep=",", inferSchema=True)
```

**Ver informações do DF**: `df.printSchema()`

**Listar arquivos que estão no DBFS**: `%fs ls /caminho`

**Informações de um arquivo**: `%fs head /caminho`

#### JSON

**Carregando mais de um arquivo json (com mesma estrutura) para um DF**:

```py
%python
df = spark.read.json(['caminho1', 'caminho2'])
```

**Carregando todos arquivos json (com mesma estrutura) para um DF**:

```py
%python 
df = spark.read.json("caminho/*.json") 
```

**Transformar um DF em arquivo**

```py
df.write.json("/caminho")
```

**Criação de uma View a partir de arquivos Json e consultá-la (melhor performance)**

```py
%python
spark.sql("CREATE OR REPLACE TEMPORARY VIEW nome_view USING json OPTIONS" +
          " (path '/caminho')")
spark.sql("select coluna from nome_view")
```

#### Parquet

**Gravando um DF em um parquet**: `df.write.parquet("/caminho")`

**Sobrescrever um parquet**: `df.write.mode('overwrite').parquet('/caminho')`

**Ler arquivo parquet e guardar em um DF**: `df.read.parquet('/caminho')`

**Consulta SQL a partir desse DF**:

```py
df.createOrReplaceTempView('view_parquet')
resultadoSQL = spark.sql("select * from view_parquet")
```
