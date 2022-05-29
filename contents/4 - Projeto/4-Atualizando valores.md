# 4.4 - Atualizando valores

Atualizar dados é algo importante que precisamos ter quando criamos aplicações. 

Para atualizarmos um dado no PostgreSQL, precisamos usar o comando `UPDATE` nas tabelas.

Vamos alterar a descrição de um produto em específico:

```bash
myecommerce=# UPDATE products SET description = 'Computador AMD' WHERE id = 1;
UPDATE 1
myecommerce=#
```

Usamos o `SET` description = 'Computador AMD' para determinar que a descrição irá mudar. Com o `WHERE` (onde) o id for igual á '1'. E por fim, `UPDATE` é um comando bem simples como você pode ver.

Vale ressaltar, que se a gente não tivese colocado o comando `WHERE` ele teria alterado todas as descrição de todos os produtos.

<br/>
<div style="text-align: right">

[Próxima página](/contents/4%20-%20Projeto/5-Deletando%20valores.md)

</div>