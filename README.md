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

![alt text](./imgs/image.png)

#### Metodologia de Autenticação Comum:

> `trust`: Conexões são permitidas sem senha.

> `md5` : Utiliza MD5 para encriptar senhas.

> `password`: Senha é enviada em texto plano.

> `reject`: Rejeita todas as conexões correspondentes.

#### Melhores Práticas:

> Utilize sub-redes específicas em vez de permitir conexões de qualquer IP.

> Combine métodos de autenticação robustos como `md5` ou `scram-sha-256`

> Mantenha o arquivo organizado e documentado para fácil manutenção.

## Backup e Recuperação no PostgreSQL

### Tipos de backup

> Lógico: O backup lógico consiste em exportar os dados do banco de dados em um formato legível (geralmente SQL), que pode ser importado em um banco de dados.

> `pg_dump` -U nome_do_usuario -d nome_do_banco -F c -b -v -f arquivo.backup

> `pg_restore` -U nome_do_usuario -d nome_do_banco -v arquivo.backup

> Físico: O backup físico envolve copiar diretamente os arquivos do banco de dados no sistema de arquivos. Isso inclui todos os arquivos de dados, logs de transação, e outros arquivos essenciais para o funcionamento do banco de dados.

> `pg_basebackup`-D /caminho/para/backup -Ft -z -P

### Detalhamento do `pg_dump`

> -U nome_do_usuario: Especifica o nome do usuário que irá se conectar ao banco de dados. Exemplo: `-U postgres` indica que o usuário `postgres` será utilizado para a conexão.

> -d nome_do_banco: Especifica o nome do banco de dados do qual será feito o backup. Exemplo: `-d meu_banco` indica que o banco de dados `meu_banco` será alvo do backup.

> -F c: Define o formato do arquivo de backup. - `c` significa "custom", um formato de backup personalizado que pode ser restaurado usando a ferramenta `pg_restore`. Outros formatos possíveis incluem `t` (tar) e `p` (plain text).

> -b: Inclui grandes objetos (blobs) no backup. Útil se o banco de dados contém dados binários armazenados como grandes objetos.

> -v: Ativa o modo verboso, que faz com que o `pg_dump` mostre mais informações durante o processo de backup. Útil para monitorar o progresso e diagnosticar problemas.

> -f arquivo.backup: Especifica o nome do arquivo onde o backup será salvo. Exemplo: `-f meu_backup.backup` salva o backup no arquivo `meu_backup.backup`.

## Mapeamento objeto relacional (ORM – Object/Relational Mapping)

![alt text](./imgs/img2.png)

> ORM é uma técnica que conecta o modelo de objetos de uma aplicação com um banco de dados relacional.

> Permite que desenvolvedores interajam com o banco de dados usando paradigmas orientados a objetos.

> Facilita a manipulação de dados através de objetos, evitando SQL manual.

> Possibilita a manutenção do paradigma da Orientação à Objetos além da camada de controle.

(osvaldo requiao melo jgp4ojhh4jo)

### Vantagens da ORM

> Produtividade: Diminui a quantidade de código necessário para interagir com o banco de dados.

> Manutenibilidade: Facilita a manutenção do código, pois separa lógica de negócio de acesso a dados.

> Portabilidade: Facilita a migração entre diferentes bancos de dados relacionais.

### Desvantagens do ORM

> Curva de Aprendizado: Pode ser complexo aprender e configurar corretamente.

> Performance: Pode introduzir overhead em operações simples.

> Flexibilidade: Algumas consultas complexas podem ser mais difíceis de implementar com ORM.

![alt text](./imgs/ORM.png)
