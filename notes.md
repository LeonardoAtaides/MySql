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