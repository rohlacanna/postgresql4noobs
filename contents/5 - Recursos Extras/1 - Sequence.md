# 5.1 - Sequence

## O que é o SEQUENCE?

Bom, se você já veio de outras `SGBD` de mercado que a gente tem como MySQL, MariaDB e como outros também, você já conhece a propriedade `AUTO_INCREMENT` que é aquela propriedade que a gente utiliza em campos do tipo inteiro para que a cada um novo registro da tabela ele vai somando `1+1`. Deste modo, fazendo com que a gente nunca tenha registros duplicados dentro da nossa base de dados.

O procedimento aqui é basicamente que o mesmo, porém aqui a gente trabalha com o conceito de `SEQUENCE` e precisamos criar ela antes, ou seja, temos que deixar a estrutura pronta para que quando a gente vá criar a nossa tabela a gente utilize ela como valor padrão do nosso campo. 

O comportamento final vai ser exatamente o mesmo, mas o processo de criação é um pouco diferente e mesmo que pareça ser mais trabalhoso notaremos que além de nós dar maiores recursos teremos uma maior organização do nosso banco de dados.

## Agora vamos ver como utiliza a `SEQUENCE` dentro do postgreSQL.

Como dito anteriomente, se você já conhece um pouco de MySQL, MariaDB provavelmente você já viu como funciona o campo `AUTO_INCREMENT` que é uma propriedade que você vai utilizar para os campos do tipo numéricos que são números sequenciais que a cada registro de dados esse número sequencial começa a se auto incrementar para que não tenha nenhum valor repetido dentro da tabela.

No postgreSQL trabalhamos usando o `SEQUENCE` ele é um pouco diferente, ele vai dar um pouco mais de flexibilidade, iremos definir qual será o valor mínimo e máximo que ela pode ter, iremos definir também o incremento que no caso o padrão é de 1 em 1. Mas, é você quem defini isso, por tanto teremos mais flexibilidade. E por fim, quando vamos criar nossa tabela, a gente seta que o valor padrão deste campo é um `nextval` ou seja, um próximo valor desta `SEQUENCE` que criamos anteriormente.

Temos um atalho também para isto, que a gente pode criar de uma maneira bastante simples. Para que a gente possa fazer um exemplo prático aqui neste curso, primeiro vamos ver a maneira mais difícil que é a maneira mais completa que temos para compreender de fato quais são as etapas e os processos que são feitos quando estamos utilizando um campo deste tipo no postgreSQL e depois faremos com a maneira mais rápida utilizando uma espécie de atalho.

Dito isso, é importante que tenha conhecimento desta duas metodologias pois, dependendo da versão que você for executar pode ser que isso mude. Portante, é ideial que tenha conhecimento, mesmo que você não utilize um deles, mas que você saiba como funciona e principalmente como identificar isso dentro da documentação.

Este curso será baseado na [documentação](https://www.postgresql.org/docs/current/sql-createsequence.html) oficial do postgreSQL.

---

Agora chega de papo e bora para a prática.

Vamos usar a sintaxe que a própria documentação disponibiliza.

O primeiro passo é identificar quais são os pontos que precisamos utilizar de fato.

###### SINTAXE PARA CRIAÇÃO DA NOSSA SEQUENCE

```
CREATE [ TEMPORARY | TEMP ] SEQUENCE [ IF NOT EXISTS ] name
    [ AS data_type ]
    [ INCREMENT [ BY ] increment ]
    [ MINVALUE minvalue | NO MINVALUE ] [ MAXVALUE maxvalue | NO MAXVALUE ]
    [ START [ WITH ] start ] [ CACHE cache ] [ [ NO ] CYCLE ]
    [ OWNED BY { table_name.column_name | NONE } ]
```

- **CREATE**: De fato vamos precisar utilizar este comando para a criação da nossa sequence.
- **[ TEMPORARY | TEMP ]**: Podemos ver que este comando tá entre colchetes que significa que é um comando opcional e quando temos um pipe `|` devemos escolher ou um ou outro. Elas são a mesma coisa, então quando queremos criar uma sequence temporária, podemos utiliar `TEMPORARY` ou `TEMP` o que não é o nosso caso agora, então tiraremos.
- **[ IF NOT EXISTS ]**: Isto aqui vai fazer uma verificação para ver se estamos ou não duplicando nossa sequence, deixaremos este comando.
- **[ AS data_type ]**: Precisamos dizer que tipo de dados irá conter nosso campo, ele precisa ser numérico e temos algumas vertentes que podemos escolher, então temos: `smallint, integer, e bigint` normalmente é utilizado o bigint. Mas, no nosso caso vou omitir isso, pois vamos definir um `MINVALUE` e `MAXVALUE` logo, automaticamente o banco de dados vai saber qual é o campo que ele deve utilizar.
- **[ INCREMENT [ BY ] increment ]**: Como queremos utilizar uma sintaxe mais completo, vamos informa-las ela também. A palavra `BY` é opcional, poderiamos deixar ela e informar em seguida o valor que queremos na frente, mas eu também vou remover esta palavra.
- **[ MINVALUE minvalue | NO MINVALUE ] [ MAXVALUE maxvalue | NO MAXVALUE ]**: Aqui vamos definir o valor minimo e o máximo. Ou, podemos utilizar o `NO MINVALUE/ NO MAXVALUE` com isso não teriamos valores mínimo ou máximo. Como no meu caso eu quero informar, usarei MINVALUE/ MAXVALUE e em seguida informar os valores.
- **[ START [ WITH ] start ]**: Não iremos utilizar a palavra reservada `WITH` então, removemos a palavra e em seguida dizemos com qual valor ele irá começar.
- **[ START [ WITH ] start ] [ CACHE cache ] [ [ NO ] CYCLE ]
    [ OWNED BY { table_name.column_name | NONE ]**: Agora temos a opção de informar o cache, cyclo e quem é o dono dessa SEQUENCE. Dependendo da arquiterura que tenha no nosso banco de dados, poderiamos criar outros usúarios para evitar que outros usúarios de outra estrutura possa consumir nossa informação. Vamos utilizar somente o cache e omitir as outras informações.

Então ficou assim:

```bash
# psql -U postgres
postgres=# CREATE SEQUENCE IF NOT EXISTS teste_seq
    INCREMENT 1
    MINVALUE 1
    MAXVALUE 999999999999
    START 1
    CACHE 1;
CREATE SEQUENCE
postgres=#
```

Visualizando:

```bash
postgres=# \d
            List of relations
 Schema |   Name    |   Type   |  Owner
--------+-----------+----------+----------
 public | teste_seq | sequence | postgres
(1 row)
```

Agora vamos criar nossa tabela:

```bash
postgres=# CREATE TABLE teste (
  teste_id integer DEFAULT nextval('teste_seq'),
  name varchar(255)
);
CREATE TABLE
postgres=#
```

Ou seja, estamos criando nossa tabela `teste` com o campo `teste_id` este campo será do tipo `integer` e o valor padrão dele será um `nextval` na nossa `SEQUENCE`e por fim, criei outro campo `name` passando um `varchar` de tamanho varíavel até 255 posições.

Visualizando:

```bash
postgres=# \d
            List of relations
 Schema |   Name    |   Type   |  Owner
--------+-----------+----------+----------
 public | teste     | table    | postgres
 public | teste_seq | sequence | postgres
(2 rows)

postgres=#
```

Agora vamos inserir um novo registro no nosso banco de dados:

```bash
INSERT INTO teste (teste_id, name) VALUES ('1', 'Rômulo');
```

Porém, como nosso `teste_id` já está sendo alimentado pela `SEQUENCE` eu não preciso alimentar ele agora, então eu simplesmente removo ele e também posso remover o paramêtro `1`

Ficando assim:

```bash
INSERT INTO teste (name) VALUES ('Rômulo');
```

A única coisa que vou inserir vai ser na coluna `name` o nome `Rômulo`

Executando:

```bash
postgres=# INSERT INTO teste (name) VALUES ('Rômulo');
INSERT 0 1
postgres=#
```

Então, se agora executarmos um SELECT na nossa tabela `teste` veremos o registro:

```bash
postgres=# select * from teste;
 teste_id |  name
----------+--------
        1 | Rômulo
(1 row)

postgres=#
```

Tudo certo! Tudo funcionando :')

E se você se lembra no começo do curso, eu disse que iria mostrar um atalho para fazermos isto, para que a gente não precise criar toda essa estrutura.

Então, vou copiar o código da criação da nossa tabela e vou renomear para `teste_2` e no nosso `teste_id` vou remover todo o conteúdo e passar a palavra reservada `serial`.

Essa palavra reservada `serial` fará com que seja criado automaticamente uma `SEQUENCE` com um nome pré definido e vai trazer este tipo de dado para dentro do campo e utilizar ele como valor padrão e fazendo uso do `nextval` também.

Ficando assim:

```bash
postgres=# CREATE TABLE teste_2 (
  teste_id serial,
  name varchar(255)
);
CREATE TABLE
postgres=#
```

Inserir um registro:

```bash
postgres=# INSERT INTO teste_2 (name) VALUES ('Floki');
INSERT 0 1
postgres=#
```

Executando um SELECT na nossa tabela `teste_2`:

```bash
postgres=# select * from teste_2;
 teste_id | name
----------+-------
        1 | Floki
(1 row)

postgres=#
```

Então, temos duas tabelas `teste` e `teste_2` cada um com registro diferente e as duas sendo alimentada por uma `SEQUENCE`.

E se dermos um `\d` veremos o seguinte:

```bash
  postgres=# \d
                  List of relations
 Schema |         Name         |   Type   |  Owner
--------+----------------------+----------+----------
 public | teste                | table    | postgres
 public | teste_2              | table    | postgres
 public | teste_2_teste_id_seq | sequence | postgres
 public | teste_seq            | sequence | postgres
(4 rows)

postgres=#
```

Temos `teste_seq` que é a `SEQUENCE` que criamos anteriomente e vemos também que tem um `teste_2_teste_id_seq` ou seja, ele cria tanto com o nome da tabela (teste_2), nome do campo(teste_id) junto com a sequencia (teste_id_seq).

Desta forma, fica mais fácil da gente diagnosticar quando tivemos qualquer tipo de problema.
