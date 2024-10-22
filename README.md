<a href="https://www.linkedin.com/in/enzodelcompare">
  <img src="https://img.shields.io/badge/criador-enzodelcompare-blue">
</a>

# <a href="https://dev.mysql.com/doc/sakila/en/">Banco de Dados Sakila</a>

O banco de dados **Sakila** foi inicialmente desenvolvido por [Mike Hillyer](https://github.com/MHillyer), um ex-membro da equipe de documentação do **MySQL AB**. Ele foi criado com a intenção de fornecer um esquema padrão que possa ser usado como exemplo em livros, tutoriais, artigos, amostras e assim por diante. O banco de dados de exemplo **Sakila** também serve para destacar recursos do **MySQL**, como **Views**, **Stored Procedures** e **Triggers**.

Informações adicionais sobre o banco de dados **Sakila** e seu uso podem ser encontradas nos [fóruns](https://forums.mysql.com/) do **MySQL**.

O banco de dados de exemplo **Sakila** é o resultado do apoio e feedback da comunidade de usuários do **MySQL** e o feedback e sugestões dos usuários são sempre bem-vindos. Por favor, envie todo o feedback utilizando este [link](http://www.mysql.com/company/contact/). Para relatórios de bugs, use [MySQL Bugs](https://bugs.mysql.com/).

## Estrutura

O diagrama a seguir fornece uma visão geral da estrutura do banco de dados de exemplo **Sakila**. O arquivo de origem do diagrama (para uso com o [MySQL Workbench](https://www.mysql.com/products/workbench/)) está incluído na distribuição do **Sakila** e é nomeado como **sakila.mwb**.

<img src="imagens/sakila-schema.png">

**Tabelas:** ```actor```, ```address```, ```category```, ```city```, ```country```, ```customer```, ```film```, ```film_actor```, ```film_category```, ```film_text```, ```inventory```, ```language```, ```payment```, ```rental```, ```staff``` e ```store```

<br>

> NOTA: Para mais informações detalhadas sobre as tabelas, suas colunas e relacionamentos, acesse [+ Sakila](https://github.com/enzodelcompare/treinamento-sql/blob/main/sakila.md)

<br>

## Acesso via Docker

Para configurar o banco de dados Sakila via Docker, você pode seguir os passos indicados neste repositório: [sakiladb/mysql](https://github.com/sakiladb/mysql). Esse processo garante que você tenha o ambiente Sakila configurado em poucos minutos, simplificando a prática de consultas SQL e testes.

<br>

## Lista de Exercícios

A lista de exercícios foi projetada para cobrir os principais conceitos de SQL e análise de dados com o banco de dados Sakila. Alguns exemplos incluem:

**Selecione todos os filmes de uma categoria específica:**

   ```
       SELECT title
         FROM film
   INNER JOIN film_category
           ON film.film_id = film_category.film_id
        WHERE category_id = 1;
   ```

 **Calcule o total de vendas por lojaÇ**

   ```
     SELECT store_id,
            SUM(amount) AS total_sales
       FROM payment
   GROUP BY store_id;
   ```

Para acessar a lista completa de exercícios, clique [aqui!](https://github.com/enzodelcompare/treinamento-sql/blob/main/exercicios/exercicios.sql)
