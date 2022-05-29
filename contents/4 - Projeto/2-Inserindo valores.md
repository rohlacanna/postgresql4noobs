# 4.2 - Inserindo valores

Após criar as tabelas com seus relacionamentos, como fizemos na lição passada, estamos prontos para começar a inserir dados no banco (registros). Para tal empregamos o comando SQL **INSERT INTO**.

## Produtos

Para inserirmos um produto, 

```bash
myecommerce=# INSERT INTO products(id, name, description)
VALUES(1, 'Computador', 'Computador INTEL');
INSERT 0 1
```

Estamos inserindo o produto computador com seu respectivo código  01 e sua descrição.

Se quisermos visualizar os dados, usamos o comando:

```bash
myecommerce=# SELECT * FROM products;
 id |    name    |   description
----+------------+------------------
  1 | Computador | Computador INTEL
(1 row)

myecommerce=#
```

<br/>
<div style="text-align: right">

[Próxima página](/contents/4%20-%20Projeto/3-Selecionando%20valores.md)

</div>