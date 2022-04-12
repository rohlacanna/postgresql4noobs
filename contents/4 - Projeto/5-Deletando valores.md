# 4.5 - Deletando valores

Agora vamos aprender a última operação principal do PostgreSQL, a operação de remoção, ou delete.

Podemos deletar valores de nossas tabelas caso fossem inseridos erroneamente ou que não vão ser mais utilizados. 

Para deltarmos um dado no PostgreSQL, precisamos usar o comando `DELETE`, especificar a tabela que queremos entrar e usar o `WHERE` para especificarmos quem queremos deletar (uma ou mais linhas).

Exemplo:

```bash
myecommerce=# DELETE FROM products WHERE description = 'Computador AMD';
DELETE 1
```

Na query acima, deletamos exclusivamente o produto com a descrição 'Computador AMD', se não utilizassemos o comando WHERE deletariamos todos os produtos da tabela.