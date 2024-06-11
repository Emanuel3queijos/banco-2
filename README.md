# Banco 2

## Catálogo de SGBD

> conjunto de tabelas que armazena a estrutura de banco de dados

### Principais components:

> Tabelas, esquemas, índices, tipos de dados, funções, armazenados nas classes:

> sql pg_class, pg_tables, pg_indexes, pg_type

```sql

SELECT * FROM pg_tables WHERE schemaname = 'public';


```

## Administração de SGBD: Controle de Acesso

> Controle de acesso envolve gerenciar quem pode acessar e manipular dados no banco.

> Métodos: ACLs (Access Control Lists), GRANT e REVOKE comandos.

```sql

ALTER DEFAULT PRIVILEGES IN SCHEMA nome_do_esquema GRANT SELECT ON TABLES TO nome_do_papel;


```

## Administração de Usuários no PostgreSQL

```sql


  CREATE USER nome_do_usuario WITH PASSWORD 'senha';


  ALTER USER nome_do_usuario WITH PASSWORD 'nova_senha';


  DROP USER nome_do_usuario;


  GRANT SELECT ON tabela TO nome_do_usuario;


```

## Administração de Papéis no PostgreSQL

> Papéis são conjuntos de permissões que podem ser atribuídos aos usuários.

```sql


CREATE ROLE nome_do_papel;

GRANT nome_do_papel TO nome_do_usuario;

REVOKE nome_do_papel FROM nome_do_usuario;


```

## Administracao de provilegios

```sql

GRANT SELECT, INSERT ON tabela TO nome_do_papel;


```

> ## Revogacao de Direitos

```sql

REVOKE SELECT ON tabela FROM nome_do_usuario;


```

> Utilização de `pg_hba.conf` para Controle de Acesso a Nível de Conexão

> O pg_hba.conf é o arquivo de configuração de Host-Based Authentication (HBA) do PostgreSQL.

> Define quais usuários podem se conectar, de quais hosts e com quais métodos de autenticação.

> Utilização de `pg_hba.conf` para Controle de Acesso a Nível de Conexão

#### Estrutura do Arquivo:

> Tipo de Conexão: `local`, `host`, `hostssl`, `hostnossl`

> Banco de Dados: Nome do banco de dados ou `all`

> Usuário: Nome do usuário ou `all`

> Endereço: Endereço IP ou sub-rede
> (apenas para tipos `host`)

> Método: Método de autenticação (`md5`, `password`, `trust`, `reject`, etc.)

# Permitir conexões locais sem senha
local   all             all                                     trust

# Permitir conexões de qualquer IP na rede 192.168.1.0/24 com autenticação MD5
host    all             all             192.168.1.0/24          md5

# Permitir conexões do IP 203.0.113.1 ao banco de dados 'meubanco' com autenticação MD5
host    meubanco        all             203.0.113.1/32          md5

# Rejeitar todas as outras conexões
host    all             all             all                     reject
