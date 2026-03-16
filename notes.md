# MY SQL

## Diferença entre SQL e No SQL
O SQL é uma linguagem para o banco de dados *relacionais*, o NoSQl é um bd *não relacional*

SQL : é possível verificar, inserir, remover, alterar os dados dentro de um *bd relacional*, ele funciona com tabelas de forma organizada
Ex:

_____nome______     _____Produto____            ______Venda_____
| 1 - Ataides |     |    1-Pão     |            | 1  | 2 | 7,50 | -> valor
|_____________|     |    2- Ovo    |            |_|____|________|
                    |______________|             |    |-> cód produto
                                                  |-> cód cliente

**Quanto maior as tabelas mais demorada as requisões dentro do bd criado**

NoSQL: Armazema informação em um tipo de documento diferentes, como o json, se destaca pela *velocidade e consegue armazenar ainda mais dados* tal quantidade se e superior de uma SQL
Ex: Redes Socias: X, Facebook, Instagram, armazenam as prefências de seus usuários em Database *NoSQL( Não relacionais)*

# Conceitos
*Primary Key* -  é chave identificadora dentro de uma tabela
*Foreign Key* - é uma chave estrangeira que vem de outra tabela
*Coluna* -  cada tipo de dado que obtem atributos dentro
*Tupla* - são dados dentro de uma linha de uma tabela
*Data value* - é um valor especifico dentro de uma tupla

# Operadores
São combinados com o WHERE para se usar uma busca mais eficiente
diferente de -- !=  |  <>
maior que -- >
menor que -- <
maior ou igual --  <=  |  >=
menos --   -

*AND* - um dado mais o outro
Ex: select * from address where address_id AND city_id;


*OR* - busca um dado ou outro
Ex: SELECT * FROM address WHERE district OR city_id;


*NOT* - nega toda a pesquisa, retorndo os valores diferentes do escolhido
Ex: SELECT * FROM address WHERE NOT district IN ('Alberta', 'Texas');

*IN*  - lista valores dentro de uma coluna
Ex: SELECT * FROM address WHERE district IN ('Alberta', 'Texas');

**Busca com *Operadores***:
Ex: SELECT * FROM customer WHERE store_id = 1 AND active != 0;

# Comandos

*USE* - seleciona o banco de dados desejado   |     Ex: USE Banco_Exemplo

*FROM* - destina da onde o dado vai vir, usado geralmente com *SELECT*

*SELECT* - seleciona algo desejado            |     Ex: SELECT CLIENT_ID FROM CLIENT
- Pode passar mais de uma coluna para trazer os dados dentro delas
Ex: SELECT ID, NAME, YEARS FROM CLIENT

- Pode listar também todas ao mesmo tempo
Ex: SELECT * FROM CLIENT

*ORDER BY*- ordena os dados dentro de uma tabela , geralmente usado com SELECT
Ex: SELECT actor_id, first_name, last_name FROM actor ORDER BY first_name;

- Temos como filtar pelo maior e menor  Ex: ORDER BT amount ( desc or asc )
- *ASC* - do menor para maior
- *DESC* - do maior para o menor

*WHERE* - direciona onde buscar o dado, passando oque deseja buscar, tanto como  strings quanto valores númericos
Ex: SELECT * FROM actor where actor_id = 1;
    SELECT * FROM address where district = 'California';

*AS* - pode nomear uma tabela criada apartir de outra
Ex: 
SELECT customer_id, amount,
 amount  - (amount * 0.10) AS '10% discount' -> passa o nome desejado
 FROM payment WHERE customer_id = 1;

*BETWEEN* - serve para filtrar de onde dar inicio, seria como um "entre" 
Ex: SELECT * FROM payment WHERE amout BETWEEN 1.99 AND 3.99;


*LIKE* - Analisa dentro de um campo, qual dado se inicia ou finaliza de acordo com a escolha, como um filtro

Ex: SELECT * FROM actor WHERE first_name LIKE 'a'; -> faz a busca apenas da letra A

- Para buscar algo que inicia com a letra desejada coloca %, que buscará algo que inicie com a letra desejada.
Ex: SELECT * FROM actor WHERE first_name LIKE 'a%';

- Passando do lado direito ele busca pela palavra que finaliza com a letra escolhida
Ex: SELECT * FROM actor WHERE first_name LIKE '%c';

*IS NULL* - Serve para denominar um campo vazio, aguarda receber um dado 
Para puxar e verificar campos que estão vazios:
Ex: SELECT * FROM address WHERE address2 IS NULL;

*LIMIT* - Serve para listar de forma mais especifica, podendo escolher de onde começar
Ex: SELECT * FROM actor LIMIT 2, 10;

*REGEXP* - Serve para realizar um mix de várias expressões para ter um resultado eficiente, bem parecido com o a expressão like, mudando apenas os comandos
Ex: SELECT * FROM actor WHERE first_name REGEXP '^a';

_Pode busca por mais inicias_
Ex: SELECT * FROM actor WHERE first_name REGEXP '^a|^b|^c';

_Pode buscar por combinação_ (Como ligação de chuveiro)
Ex: SELECT * FROM actor WHERE first_name REGEXP '[ge]a';

## INNER JOIN
Serve para filtrar os dados de múltiplas tabelas, dando uma saida em tabela parecido com o do SELECT
Ex: SELECT * FROM customer JOIN payment ON customer.customer_id = payment.payment_id LIMIT 10

### FILTRO NO INNER JOIN
Para isso puxa passando on prefixo da tabela, nome da tabela Ex: *Table.name_column*, como ficaria com o exemplo anterior
Ex:
SELECT 
    customer.customer_id,
    customer.first_name,
    customer.last_name,
    payment.rental_id,
    payment.amount
FROM customer
JOIN payment ON customer.customer_id = payment.payment_id

**A ORDEM IMPORTA DOS PREFIXOS, AO ALTERAR QUANDO E BUSCAR A COLUNA FICA DE ACORDO COM OQUE FOI PASSADO**

## ALIAS
Serve para otimizar a escrita vai ser um apelido que é dado a tabela para realizar a chamada, apenas passando o apelido na frente do nome da tabela, _Ex: customer cus, payment pay_, ficando um código mais limpo e de fácil visualização
Ex:
SELECT 
    cus.customer_id,
    cus.first_name,
    cus.last_name,
    pay.rental_id,
    pay.amount
FROM customer cus
 JOIN payment pay ON cus.customer_id = pay.payment_id

 
## INSERT 
Serve para incluir valores a uma tabela
Ex:
        |-> para se referir para a tabela
INSERT INTO language
VALUES(DEFAULT, 'Portuguese', '2008-02-20 05:02:19');
        |-> sem valor pois a tabela tem auto increment

**PARA INSERÇÃO MÚLTIPLA E APENAS DUPLICAR E SEPARAR POR VÍRGULAS**
EX:
VALUES
(DEFAULT, 'Spain', '2008-02-20 01:05:19'),
(DEFAULT, 'English', '2002-02-24 02:06:12'),
(DEFAULT, 'Italian', '2005-02-21 04:08:10')
;

**INSERÇÃO MÚLTIPLA COM DUAS TABELAS**
Ex:
INSERT INTO country
VALUES (DEFAULT, 'Brazil', '2008-02-20 05:02:19');
INSERT INTO city
VALUES (DEFAULT, 'São Paulo', last_insert_id(), '2005-02-21 05:02:19' );
                                    |-> pega o último registro de id da tabela

# COPIAR UMA TABELA - BACKUP
Realiza uma copia da tabela, por alterações não seguras ou apenas como uma copia
Ex:
CREATE TABLE payment_backup AS SELECT * FROM payment
                |-> cria uma nova tabela com as informações de outra

# REMOVER UMA TABELA
Serve para remover uma tabela por completo, ou apenas parcialmente, apenas os dados
Ex:
DROP TABLE nome_da_tabela | apaga por completo
TRUNCATE TABLE nome_da_tabela | apaga os dados dentro das colunas

OBS: com o botão direito no workbench e possível apagar também, aparecendo essas opções

# ATUALIZAR UM VALOR (REGISTRO)
Serve para atualizar um valor dentro da tabela do 
Ex:

UPDATE payment SET amount = 5.99 WHERE payment_id = 1
