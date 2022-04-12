# 4.3 - Selecionando valores

Para selecionar dados em bancos de dados PostgreSQL usamos o `SELECT`.

Digite:

```bash
SELECT * FROM products;
```

Com esse comando ele vai retornar todos os produtos que foram inseridos.

Entretanto, para consultas são relizadas filtragens para melhor busca de dados.

Por exemplo:

Para pegarmos apenas a descrição, podemos substituir o `*` por `description`.

```bash
myecommerce=# SELECT description FROM products;
   description
------------------
 Computador INTEL
(1 row)

myecommerce=#
```

E para pegarmos apenas um registro específico da tabela, que tem o nome "Computador" podemos usar `WHERE`, que com ele, podemos pegar apenas um registro onde uma certa condição é verdadeira, segue o exemplo:

```bash
myecommerce=# SELECT name FROM products WHERE name = 'Computador';
    name
------------
 Computador
(1 row)

myecommerce=#
```

Existem muitas possibilidades que podem ser feitas usando o SELECT, junto com o JOIN. Porém, vou deixar vocês procurarem esse tipo de conteúdo por conta própria :)