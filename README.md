# data-enginner-myra

### Explicação dos resultados apresentados ao decorrer do script criado em linguagem Python, através da plataforma Jupyter Notebook:

Para este desafio, foi utilizado a interface para Python chamada PySpark, que é baseada no Apache Spark. Foi utilizada a versão 3.1.2 do Spark com Hadoop 2.7.

Após a importação dos 4 datasets em forma de dataframes, a primeira coisa a ser feita foi verificar a quantidade de linhas de cada um destes dataframes, e para isso, foi utilizado o comando pyspark.sql.DataFrame.count, que seguindo o esperado, retornou o total de linhas.

Feito isto, foi a vez de unificar os dataframes. Para unificar os datasets olist_orders_dataset.csv, olist_order_reviews_dataset.csv, olist_order_items_dataset.csv e olist_products_dataset.csv, foi utilizado o comando pyspark.sql.DataFrame.join e seus formatos.

Primeiro, foram unificados o dataframe do arquivo olist_orders_dataset.csv com o do arquivo olist_order_reviews_dataset.csv, utilizando o formato Outer Join tendo a coluna order_id como referência.

Em seguida, o dataframe resultante da 1ª unificação, foi unificado com o dataframe do arquivo olist_order_items_dataset.csv, novamente utilizando o format Outer Join e a coluna order_id. E por último, foi feita a unificação do 2º dataframe resultante com o dataframe do arquivos olist_products_dataset.csv, mas desta vez utilizando o formato Left e a coluna product_id.
Tanto o formato Outer, quanto o Left, apresentaram o mesmo resultado neste caso, mas como a referência de dados estava inteira na 1ª tabela, optou-se por utilizar o Left. Com isso, foi gerado o dataframe unificado final.

Logo depois foi a vez de obter o total de linhas de acordo com a coluna product_category_name, e retornando somente os 10 primeiros resultados em ordem decrescente. Para isso, foi utilizado os comandos pyspark.sql.DataFrame.count e pyspark.sql.DataFrame.sort.

Depois disso, foi a vez de remover todas as colunas com "id" no nome. Para identificar-se os nomes das colunas sem erro, optou-se por verificar o schema do dataframe unificado final, por meio do comando pyspark.sql.DataFrame.printSchema.
Tendo em mãos os nomes das colunas que seriam excluídas, foi utilizado o comando pyspark.sql.DataFrame.drop e em seguida o schema foi verificado novamente para confirmar a exclusão.

Em seguida, a coluna review_creation_date foi convertida para o tipo Date, através dos comandos pyspark.sql.DataFrame.withColumn e pyspark.sql.Column.cast.

Adiante foi criada uma função que converte todos os textos de todas as colunas para minúsculo. Esta função faz uso de 1 laço FOR e de 2 comandos: pyspark.sql.DataFrame.withColumn e pyspark.sql.functions.lower.

Logo após, outra função foi criada, mas dessa vez para procurar determinadas palavras e criar uma coluna extra, contendo a classificação de acordo com a palavra encontrada. Para isto, a função faz uso de de um laço FOR e 3 comandos: pyspark.sql.DataFrame.withColumn, pyspark.sql.functions.when e pyspark.sql.Column.rlike.
Para a contagem das linhas desta nova coluna, foi utilizado os comandos pyspark.sql.DataFrame.count e pyspark.sql.DataFrame.groupBy.

Em seguida, foram criados 2 gráficos, um de pizza e outro de barras, utilizando a biblioteca Matplotlib e os comandos pyspark.sql.DataFrame.select e pyspark.sql.DataFrame.collect.

Por conseguinte, foi feita a soma da coluna “price” agrupando os valores pela coluna produto_category_name e retornando os 6 maiores valores, em ordem decrescente. Neste caso, foram utilizados comandos pyspark.sql.DataFrame.groupBy e pyspark.sql.DataFrame.agg.

Por último, foi gerado um gráfico de barras, novamente utilizando a biblioteca Matplotlib e os comandos pyspark.sql.DataFrame.select e pyspark.sql.DataFrame.collect.

Para finalizar, a sessão do Spark foi encerrada.
