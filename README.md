# Netbox
Sistema de documentação de Infraestrutura de rede



# Instalação do banco de dados PostgreSQL

Esta seção envolve a instalação e configuração de um banco de dados PostgreSQL local. Se você já possui um serviço de banco de dados PostgreSQL, pule para a próxima seção .
> O NetBox requer o PostgreSQL 10 ou posterior. Observe que MySQL e outros bancos de dados relacionais não são suportados.

### Instalação:
```bash
sudo apt update
sudo apt install -y postgresql
```
Após a instalação do PostgreSQL, inicie o serviço e habilite-o para ser executado na inicialização:
```bash
sudo systemctl start postgresql
sudo systemctl enable postgresql
```
Antes de continuar, verifique se você instalou o PostgreSQL 10 ou posterior:
```bash
psql -V
```
### Criação de banco de dados

No mínimo, precisamos criar um banco de dados para o NetBox e atribuir a ele um nome de usuário e senha para autenticação. Comece invocando o shell PostgreSQL como o usuário Postgres do sistema.

```bash
sudo -u postgres psql
```
Dentro do shell, digite os seguintes comandos para criar o banco de dados e o usuário (função), substituindo seu próprio valor pela senha:

```bash
CREATE DATABASE netbox;
CREATE USER netbox WITH PASSWORD 'J5brHrAXFLQSif0K';
GRANT ALL PRIVILEGES ON DATABASE netbox TO netbox;
```

> Não use a senha do exemplo. Escolha uma senha forte e aleatória para garantir a autenticação segura do banco de dados para sua instalação do NetBox.

Depois de concluído, digite \q para sair do shell do PostgreSQL.

### Edite os aquivos 

edite pg_hba.conf
```bash
vim /etc/postgresql/14/main/pg_hba.conf
```
e inclua a seguinte infomacao no final do arquivo
```bash
host all all 0.0.0.0/0 md5
```
e edite postgresql.conf
```bash
vim /etc/postgresql/14/main/postgresql.conf
```
> listen_addresses='*'

### Verificar status do serviço

Instale o cliente de conexao
```bash
apt install postgresql-client

```
Você pode verificar se a autenticação funciona executando o psqlcomando e passando o nome de usuário e a senha configurados. (Substitua localhost por seu servidor de banco de dados se estiver usando um banco de dados remoto.)
```bash
psql --username netbox --password --host localhost
```
# Instalar o Redis
Redis é um armazenamento de valor-chave na memória que o NetBox emprega para armazenamento em cache e enfileiramento. Esta seção envolve a instalação e configuração de uma instância local do Redis. Se você já tiver um serviço Redis, pule para a próxima seção .
> O NetBox v2.9.0 e posterior requerem Redis v4.0 ou superior. Se sua distribuição não oferecer uma versão recente o suficiente, você precisará compilar o Redis a partir da fonte. 
```bash
sudo apt install -y redis-server
```
Antes de continuar, verifique se sua versão instalada do Redis é pelo menos v4.0:
```bash
redis-server -v
```
Você pode querer modificar a configuração do Redis em /etc/redis.confou /etc/redis/redis.conf, no entanto, na maioria dos casos, a configuração padrão é suficiente.
### Verificar status do serviço
Use o redis-cliutilitário para garantir que o serviço Redis esteja funcional:
```bash
redis-cli ping
```
Se for bem-sucedido, você deverá receber uma PONG resposta do servidor.






```bash

```
