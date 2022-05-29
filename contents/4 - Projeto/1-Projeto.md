# 4.1 - Projeto

Em primeiro lugar, vamos construir uma base de dados dentro do nosso banco. Para criar um banco de dados, use o `psql` para entrar no shell interativo do PostgreSQL.

```bash
# psql -U postgres
postgres=# CREATE DATABASE myecommerce;
CREATE DATABASE
```

Você também pode usar o comando `\l` para listar e verificar se seu banco de dados realmente foi criado.

Com isso, criamos nossa base de dados denominada `myecommerce`.

Vamos acessar nosso banco de dados `myecommerce`:

```bash
# psql -U postgres myecommerce
psql (14.2 (Debian 14.2-1.pgdg110+1))
Type "help" for help.

myecommerce=#
```

Agora vamos execute essa query para criarmos a tabela:

## Produtos

```bash
myecommerce=# CREATE TABLE products (
myecommerce(# id int,
myecommerce(# name varchar(60),
myecommerce(# description varchar(150)
myecommerce(# );
CREATE TABLE
```

Criamos a tabela `products` com seu id de valor inteiro. Além disso, definimos que o `name` é um VARCHAR de valor máximo 60 caracteres e uma `description` que também é um VARCHAR de valor máximo 150 caracteres.

Para visualizar as tabelas existentes no seu banco, execute o comando:

```bash
myecommerce-# \dt
          List of relations
 Schema |   Name   | Type  |  Owner
--------+----------+-------+----------
 public | products | table | postgres
(1 row)
```

<br/>
<div style="text-align: right">

[Próxima página](/contents/4%20-%20Projeto/2-Inserindo%20valores.md)

</div>