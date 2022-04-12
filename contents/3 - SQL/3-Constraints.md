# 3.3 - Constraints

## O que são?

São restrições impostas por nós a determinadas colunas da tabela do DB.

## O que fazem?

Definem restrições para as colunas.

## Quais são?

Existem diversos tipos de constraints (restrições) que podemos aplicar as nossas colunas, algumas delas são:

`NOT NULL` - O campo com essa restrição nunca poderá ser nulo, caso haja um valor padrão, ele será atribuído, caso contrário iremos precisar informar um valor.

`UNIQUE` - Faz com que o valor inserido na coluna seja único, nunca poderá haver outro valor igual

`PRIMARY KEY` - Garante com que a coluna seja usada como identificador único da tabela, também faz com que a coluna não possa receber valores nulos ou repetidos.

`FOREIGN KEY` - Faz referência a chave primária de outra tabela, permitindo assim o relacionamento entre colunas.

`DEFAULT` - Garante que um valor padrão seja passado, sempre que determinada coluna receber valor nulo em sua criação ou manipulação.