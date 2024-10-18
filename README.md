<a href="https://www.linkedin.com/in/enzodelcompare">
  <img src="https://img.shields.io/badge/criador-enzodelcompare-blue">
</a>

# Banco de Dados Sakila

O banco de dados **Sakila** foi inicialmente desenvolvido por [Mike Hillyer](https://github.com/MHillyer), um ex-membro da equipe de documentação do **MySQL AB**. Ele foi criado com a intenção de fornecer um esquema padrão que possa ser usado como exemplo em livros, tutoriais, artigos, amostras e assim por diante. O banco de dados de exemplo **Sakila** também serve para destacar recursos do **MySQL**, como **Views**, **Stored Procedures** e **Triggers**.

Informações adicionais sobre o banco de dados **Sakila** e seu uso podem ser encontradas nos [fóruns](https://forums.mysql.com/) do **MySQL**.

O banco de dados de exemplo **Sakila** é o resultado do apoio e feedback da comunidade de usuários do **MySQL** e o feedback e sugestões dos usuários são sempre bem-vindos. Por favor, envie todo o feedback utilizando este [link](http://www.mysql.com/company/contact/). Para relatórios de bugs, use [MySQL Bugs](https://bugs.mysql.com/).

## Estrutura

O diagrama a seguir fornece uma visão geral da estrutura do banco de dados de exemplo **Sakila**. O arquivo de origem do diagrama (para uso com o [MySQL Workbench](https://www.mysql.com/products/workbench/)) está incluído na distribuição do **Sakila** e é nomeado como **sakila.mwb**.

<img src="imagens/sakila-schema.png">

**Tabelas:** ```actor```, ```address```, ```category```, ```city```, ```country```, ```customer```, ```film```, ```film_actor```, ```film_category```, ```film_text```, ```inventory```, ```language```, ```payment```, ```rental```, ```staff``` e ```store```

<br>

## Tabela [actor](https://dev.mysql.com/doc/sakila/en/sakila-structure-tables-actor.html)

- A tabela ```actor``` lista informações de todos os atores.
- A tabela actor é associada à tabela ```film``` por meio da tabela ```film_actor```.

**Colunas:**

- **actor_id:** Uma chave primária usada para identificar exclusivamente cada ator na tabela.
- **first_name:** O primeiro nome do ator.
- **last_name:** O sobrenome do ator.
- **last_update:** Quando a linha foi criada ou atualizada pela última vez.

<br>

## Tabela [address](https://dev.mysql.com/doc/sakila/en/sakila-structure-tables-address.html)

- A tabela ```address``` contém informações de endereço para clientes, funcionários e lojas.
- A chave primária da tabela ```address``` aparece como chave estrangeira nas tabelas ```customer```, ```staff``` e ```store```.

**Colunas:**

- **address_id:** Uma chave primária usada para identificar exclusivamente cada endereço na tabela.
- **address:** A primeira linha de um endereço.
- **address2:** Uma segunda linha opcional de um endereço.
- **district:** A região de um endereço, que pode ser um estado, província, prefeitura, etc.
- **city_id:** Uma chave estrangeira apontando para a tabela city.
- **postal_code:** O código postal ou CEP do endereço (quando aplicável).
- **phone:** O número de telefone do endereço.
- **last_update:** Quando a linha foi criada ou atualizada pela última vez.
- **location:** Uma coluna de geometria com um índice espacial.

> **Nota:** A coluna de localização espacial é suportada a partir do **MySQL 5.7.5**. Esta coluna é adicionada apenas ao executar os arquivos **SQL** do **Sakila** no servidor **MySQL 5.7.5** e superior. Adicionalmente, a chave espacial ```SPATIAL KEY idx_location``` também é adicionada.

<br>

## Tabela [category](https://dev.mysql.com/doc/sakila/en/sakila-structure-tables-category.html)

- A tabela ```category``` lista as categorias que podem ser atribuídas a um filme.
- A tabela ```category``` é associada à tabela ```film``` por meio da tabela ```film_category```.

**Colunas:**

- **category_id:** Uma chave primária usada para identificar exclusivamente cada categoria na tabela.
- **name:** O nome da categoria.
- **last_update:** Quando a linha foi criada ou atualizada pela última vez.

<br>

## Tabela [city](https://dev.mysql.com/doc/sakila/en/sakila-structure-tables-city.html)

- A tabela ```city``` contém uma lista de cidades.
- A tabela ```city``` é referenciada por uma chave estrangeira na tabela ```address``` e refere-se à tabela ```country``` usando uma chave estrangeira.

**Colunas:**

- **city_id:** Uma chave primária usada para identificar exclusivamente cada cidade na tabela.
- **city:** O nome da cidade.
- **country_id:** Uma chave estrangeira identificando o país ao qual a cidade pertence.
- **last_update:** Quando a linha foi criada ou atualizada pela última vez.

<br>

## Tabela [country](https://dev.mysql.com/doc/sakila/en/sakila-structure-tables-country.html)

- A tabela ```country``` contém uma lista de países.
- A tabela ```country``` é referenciada por uma chave estrangeira na tabela ```city```.

**Colunas:**

- **country_id:** Uma chave primária usada para identificar exclusivamente cada país na tabela.
- **country:** O nome do país.
- **last_update:** Quando a linha foi criada ou atualizada pela última vez.

<br>

## Tabela [customer](https://dev.mysql.com/doc/sakila/en/sakila-structure-tables-customer.html)

- A tabela ```customer``` contém uma lista de todos os clientes.
- A tabela ```customer``` é referenciada nas tabelas ```payment``` e ```rental``` e refere-se às tabelas ```address``` e ```store``` usando chaves estrangeiras.

**Colunas:**

- **customer_id:** Uma chave substituta usada para identificar exclusivamente cada cliente na tabela.
- **store_id:** Uma chave estrangeira identificando a "loja de origem" do cliente. Os clientes não estão limitados a alugar apenas nesta loja, mas esta é a loja onde geralmente compram.
- **first_name:** O primeiro nome do cliente.
- **last_name:** O sobrenome do cliente.
- **email:** O endereço de e-mail do cliente.
- **address_id:** Uma chave estrangeira identificando o endereço do cliente na tabela address.
- **active:** Indica se o cliente está ativo. Definir isso como FALSE serve como uma alternativa para excluir o cliente completamente. A maioria das consultas deve ter uma cláusula WHERE active = TRUE.
- **create_date:** A data em que o cliente foi adicionado ao sistema. Esta data é automaticamente definida usando um trigger durante uma inserção.
- **last_update:** Quando a linha foi criada ou atualizada pela última vez.

<br>

## Tabela [film](https://dev.mysql.com/doc/sakila/en/sakila-structure-tables-film.html)

- A tabela ```film``` é uma lista de todos os filmes potencialmente em estoque nas lojas. As cópias reais em estoque de cada filme estão representadas na tabela ```inventory```.
- A tabela ```film``` refere-se à tabela ```language``` e é referenciada pelas tabelas ```film_category```, ```film_actor``` e ```inventory```.

**Colunas:**

- **film_id:** Uma chave primária usada para identificar exclusivamente cada filme na tabela.
- **title:** O título do filme.
- **description:** Uma breve descrição ou resumo da trama do filme.
- **release_year:** O ano em que o filme foi lançado.
- **language_id:** Uma chave estrangeira apontando para a tabela language; identifica o idioma do filme.
- **original_language_id:** Uma chave estrangeira apontando para a tabela language; identifica o idioma original do filme. Usado quando um filme foi dublado para um novo idioma.
- **rental_duration:** A duração do período de locação, em dias.
- **rental_rate:** O custo para alugar o filme pelo período especificado na coluna rental_duration.
- **length:** A duração do filme, em minutos.
- **replacement_cost:** O valor cobrado ao cliente se o filme não for devolvido ou for devolvido danificado.
- **rating:** A classificação atribuída ao filme. Pode ser uma das seguintes: G, PG, PG-13, R ou NC-17.
- **special_features:** Lista quais recursos especiais comuns estão incluídos no DVD. Pode ser zero ou mais dos seguintes: Trailers, Comentários, Cenas Excluídas, Bastidores.
- **last_update:** Quando a linha foi criada ou atualizada pela última vez.

<br>

## Tabela [film_actor](https://dev.mysql.com/doc/sakila/en/sakila-structure-tables-film_actor.html)

- A tabela ```film_actor``` é usada para suportar uma relação muitos-para-muitos entre filmes e atores. Para cada ator em um determinado filme, haverá uma linha na tabela ```film_actor``` listando o ator e o filme.
- A tabela ```film_actor``` refere-se às tabelas ```film``` e ```actor``` usando chaves estrangeiras.

**Colunas:**

- **actor_id:** Uma chave estrangeira identificando o ator.
- **film_id:** Uma chave estrangeira identificando o filme.
- **last_update:** Quando a linha foi criada ou atualizada pela última vez.

<br>

## Tabela [film_category](https://dev.mysql.com/doc/sakila/en/sakila-structure-tables-film_category.html)

- A tabela ```film_category``` é usada para suportar uma relação muitos-para-muitos entre filmes e categorias. Para cada categoria aplicada a um filme, haverá uma linha na tabela ```film_category``` listando a categoria e o filme.
- A tabela ```film_category``` refere-se às tabelas ```film``` e ```category``` usando chaves estrangeiras.

**Colunas:**

- **film_id:** Uma chave estrangeira identificando o filme.
- **category_id:** Uma chave estrangeira identificando a categoria.
- **last_update:** Quando a linha foi criada ou atualizada pela última vez.

<br>

## Tabela [film_text](https://dev.mysql.com/doc/sakila/en/sakila-structure-tables-film_text.html)

- A tabela ```film_text``` contém as colunas ```film_id```, ```title``` e ```description``` da tabela ```film```, com o conteúdo da tabela mantido em sincronia com a tabela ```film``` por meio de **triggers** nas operações ```INSERT```, ```UPDATE``` e ```DELETE``` na tabela ```film```.
- Antes do servidor **MySQL 5.6.10**, a tabela ```film_text``` era a única tabela no banco de dados de exemplo **Sakila** que usava o mecanismo de armazenamento **MyISAM**. Isso ocorre porque a busca de texto completo é usada para títulos e descrições dos filmes listados na tabela ```film```. O **MyISAM** foi usado porque o suporte à busca de texto completo com **InnoDB** não estava disponível até o servidor **MySQL 5.6.10**.

**Colunas:**

- **film_id:** Uma chave primária usada para identificar exclusivamente cada filme na tabela.
- **title:** O título do filme.
- **description:** Uma breve descrição ou resumo da trama do filme.

O conteúdo da tabela film_text nunca deve ser modificado diretamente. Todas as alterações devem ser feitas na tabela film.

<br>

## Tabela [inventory](https://dev.mysql.com/doc/sakila/en/sakila-structure-tables-inventory.html)

- A tabela ```inventory``` contém uma linha para cada cópia de um determinado filme em uma determinada loja.
- A tabela ```inventory``` refere-se às tabelas ```film``` e store usando chaves estrangeiras e é referenciada pela tabela ```rental```.

**Colunas:**

- **inventory_id:** Uma chave primária usada para identificar exclusivamente cada item no inventário.
- **film_id:** Uma chave estrangeira apontando para o filme que este item representa.
- **store_id:** Uma chave estrangeira apontando para a loja que possui este item.
- **last_update:** Quando a linha foi criada ou atualizada pela última vez.

<br>

## Tabela [language](https://dev.mysql.com/doc/sakila/en/sakila-structure-tables-language.html)

- A tabela ```language``` é uma tabela de consulta listando os possíveis idiomas que os filmes podem ter para seus valores de idioma e idioma original.
- A tabela ```language``` é referenciada pela tabela ```film```.

**Colunas:**

- **language_id:** Uma chave primária usada para identificar exclusivamente cada idioma.
- **name:** O nome em inglês do idioma.
- **last_update:** Quando a linha foi criada ou atualizada pela última vez.

<br>

## Tabela [payment](https://dev.mysql.com/doc/sakila/en/sakila-structure-tables-payment.html)

- A tabela ```payment``` registra cada pagamento feito por um cliente, com informações como o valor e a locação que está sendo paga (quando aplicável).
- A tabela ```payment``` refere-se às tabelas ```customer```, ```rental``` e ```staff```.

**Colunas:**

- **payment_id:** Uma chave primária usada para identificar exclusivamente cada pagamento.
- **customer_id:** O cliente cujo saldo está sendo pago. Esta é uma referência de chave estrangeira para a tabela customer.
- **staff_id:** O funcionário que processou o pagamento. Esta é uma referência de chave estrangeira para a tabela staff.
- **rental_id:** A locação à qual o pagamento está sendo aplicado. Isto é opcional porque alguns pagamentos são para taxas pendentes e podem não estar diretamente relacionados a uma locação.
- **amount:** O valor do pagamento.
- **payment_date:** A data em que o pagamento foi processado.
- **last_update:** Quando a linha foi criada ou atualizada pela última vez.

<br>

## Tabela [rental](https://dev.mysql.com/doc/sakila/en/sakila-structure-tables-rental.html)

- A tabela ```rental``` contém uma linha para cada locação de cada item de inventário, com informações sobre quem alugou qual item, quando foi alugado e quando foi devolvido.
- A tabela ```rental``` refere-se às tabelas ```inventory```, ```customer``` e ```staff``` e é referenciada pela tabela ```payment```.

**Colunas:**

- **rental_id:** Uma chave primária que identifica exclusivamente a locação.
- **rental_date:** A data e hora em que o item foi alugado.
- **inventory_id:** O item sendo alugado.
- **customer_id:** O cliente alugando o item.
- **return_date:** A data e hora em que o item foi devolvido.
- **staff_id:** O funcionário que processou a locação.
- **last_update:** Quando a linha foi criada ou atualizada pela última vez.

<br>

## Tabela [staff](https://dev.mysql.com/doc/sakila/en/sakila-structure-tables-staff.html)

- A tabela ```staff``` lista todos os funcionários, incluindo informações sobre endereço de e-mail, informações de login e foto.
- A tabela ```staff``` refere-se às tabelas ```store``` e ```address``` usando chaves estrangeiras, e é referenciada pelas tabelas ```rental```, ```payment``` e ```store```.

**Colunas:**

- **staff_id:** Uma chave primária que identifica exclusivamente o funcionário.
- **first_name:** O primeiro nome do funcionário.
- **last_name:** O sobrenome do funcionário.
- **address_id:** Uma chave estrangeira para o endereço do funcionário na tabela address.
- **picture:** Um BLOB contendo uma fotografia do funcionário.
- **email:** O endereço de e-mail do funcionário.
- **store_id:** A "loja de origem" do funcionário. O funcionário pode trabalhar em outras lojas, mas geralmente é atribuído à loja listada.
- **active:** Indica se este é um funcionário ativo. Se os funcionários saírem, suas linhas não são excluídas desta tabela; em vez disso, esta coluna é definida como FALSE.
- **username:** O nome de usuário usado pelo funcionário para acessar o sistema de locação.
- **password:** A senha usada pelo funcionário para acessar o sistema de locação. A senha deve ser armazenada como um hash usando a função SHA2().
- **last_update:** Quando a linha foi criada ou atualizada pela última vez.

<br>

## Tabela [store](https://dev.mysql.com/doc/sakila/en/sakila-structure-tables-store.html)

- A tabela ```store``` lista todas as lojas no sistema. Todo o inventário é atribuído a lojas específicas, e funcionários e clientes são atribuídos a uma "loja de origem".
- A tabela ```store``` refere-se às tabelas ```staff``` e ```address``` usando chaves estrangeiras e é referenciada pelas tabelas ```staff```, ```customer``` e ```inventory```.

**Colunas:**

- **store_id:** Uma chave primária que identifica exclusivamente a loja.
- **manager_staff_id:** Uma chave estrangeira identificando o gerente desta loja.
- **address_id:** Uma chave estrangeira identificando o endereço desta loja.
- **last_update:** Quando a linha foi criada ou atualizada pela última vez.
