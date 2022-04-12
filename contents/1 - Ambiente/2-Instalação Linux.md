# 1.2 - Instalação no Linux

A intalação no ambiente Linux (estou utilizando Ubuntu 20.04) como por padrão é via linha de comando, então abra seu terminal e bora.

Para instalar o PostgreSQL, primeiro atualize o índice de pacotes local do seu servidor:

```bash
$ sudo apt update
```

Então, instale o pacote Postgres jutamente com um pacote `-contrib` que adiciona alguns serviços e funcionalidade adicionais:

```bash
$ sudo apt install postgresql postgresql-contrib
```

Basicamente já está instalado o PostgreSQL mas temos que configura-lo corretamente para melhor uso.

# Configuração

Após a instalação, o Postgres é configurado para usar a autenticação _ident_, o que significa que ele associa os roles com uma conta do sistema Unix/Linux que combine. Se um role existe no Postgres, um nome de usuário Unix/Linux com o mesmo nome é capaz de fazer login como aquele role.

O procedimento de instalação criou uma conta de usuário chamada **postgres** que está associada ao role padrão do Postgres. Existem algumas maneiras de utilizar essa conta para acessar o Postgres. Uma maneira é trocar para a conta **postgres** em seu servidor digitando:

```bash
$ sudo -i -u postgres
```

Em seguida, você pode acessar o prompt do Postgres digitando:

```
$ psql
```

Isso irá logar você no prompt do PostgreSQL, e daqui você está livre para interagir com o sistema de gerenciamento de banco de dados imediatamente.

Para sair do prompt do PostgreSQL, execute o seguinte:

```
postgres=# \q
```

Isso irá trazer você de volta ao prompt de comando do Linux postgres.

Você também pode executar o comando que quiser com a conta postgres diretamente com o sudo:

```bash
$ sudo -u postgres psql
```

Isso irá logar você diretamente no Postgres sem o shell bash intermediário.

Novamente, você pode sair da sessão interativa Postgres digitando:

```
postgres=# \q
```

Agora vamos fazer a criação de um novo role

Se você tiver feito o login com a conta postgres, crie um novo usuário digitando:

```bash
postgres@server:~$ createuser --interactive
```

Se, ao invés disso, você preferir usar o sudo para cada comando sem mudar da sua conta usual, digite:

```bash
$ sudo -u postgres createuser --interactive
```

De qualquer maneira, o script solicitará que você faça algumas escolhas e, com base nas suas respostas, executará os comandos corretos do Postgres para criar um usuário baseado nas suas especificações.

```bash
Output
Enter name of role to add: tomate
Shall the new role be a superuser? (y/n) y
```

Precisamos agora criar um novo banco de dados, pois o sistema de autenticação do **Postgres** faz por padrão é que para qualquer role usado para logar, esse role terá um banco de dados com o mesmo nome que ele pode acessar.

Isso significa que, se o usuário que você criou na última seção for chamado de **tomate**, esta role tentará se conectar a um banco de dados também denominado "tomate", por padrão. Você pode criar o banco de dados apropriado com o comando `createdb`.

```bash
postgres@server:~$ createdb tomate
```

Se, ao invés disso, você preferir usar o sudo para cada comando sem mudar da sua conta usual, você digitaria:

```bash
$ sudo -u postgres createdb tomate
```

Para logar com a autenticação baseada no `ident`, você precisará de um usuário Linux com o mesmo nome que seu role e banco de dados do Postgres.

Se você não tiver um usuário do Linux que combine disponível, você pode criar um com o comando adduser. Você terá que fazer isso através da sua conta não-**root** com privilégios sudo (ou seja, não logado como o usuário **postgres**):

```bash
$ sudo adduser tomate
```

Uma vez que essa nova conta estiver disponível, você pode ou mudar e se conectar ao banco de dados digitando:

```bash
$ sudo -i -u tomate
$ psql
```

Ou você pode fazer isso em linha:

```bash
$ sudo -u tomate psql
```

Este comando irá logar você automaticamente, supondo que todos os componentes tenham sido configurados corretamente.