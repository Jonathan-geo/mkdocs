#MySQL 

O MySQL é um sistema gerenciador de banco de dados relacional de código aberto. O serviço utiliza a linguagem SQL (Structure Query Language – Linguagem de Consulta Estruturada), que é a linguagem mais popular para inserir, acessar e gerenciar o conteúdo armazenado num banco de dados.O MySQL é um produto regido pela licença GPL (General Public License) portanto é "parcialmente" Open Source.
Nesta documentação utilizarei o LAMP, um acrônimo para Linux, Apache, MySQL e Perl/PHP/Python. Nesse conjunto de aplicações, inclui-se, respectivamente, um sistema operacional, um servidor web, um sistema gerenciador de banco de dados e uma linguagem de programação.

##Instalação
OBS: O sistema operacional utilizado é o Linux Ubuntu. 
Executar em ordem, no terminal:

```
#Instalando o Apache

sudo apt update 

sudo apt upgrade -y

sudo apt install -y apache2

```
Para testar se o Apache está funcionando corretamente, devemos digitar localhost na barra de endereços do navegador de sua preferência.

```
#Instalando o PHP 

sudo apt install -y php php-cli php-common php-gd php-mbstring php-intl php-xml php-zip php-pear libapache2-mod-php
```
```
#Testando o PHP

echo “<?php phpinfo(); ?>” | sudo tee /var/www/html/test.php | sudo service apache2 restart
```
Para testar o PHP no navegador, digite na página de endereços: 

>localhost/test.php

```
#Instalando o MySQL

sudo apt install -y mysql-server mysql-client php-mysql
```


```
#Acessar o MySQL no Terminal

sudo mysql
```
##Configuração 

Criar novo usuário:

```
sudo mysql 
#Ou somente mysql(depende de seu acesso)


CREATE USER 'seu_usuario'@'localhost' IDENTIFIED BY 'sua_senha';
GRANT ALL PRIVILEGES ON *.* TO 'seu_usuario'@'localhost' WITH GRANT OPTION;
```
Entrando com o usuário criado.
```
sudo mysql -u seu_usuario -p

#exit (para sair)
```
<h2>Instalando o phpMyAdmin</h2>

```
sudo apt install -y phpmyadmin
```

Para testá-lo no navegador, digite na barra de endereços: 

>localhost/phpmyadmin

Digite seu usuário e senha registrados na configuração do MySQL.

<h2>Instalação do MySQL WorkBench</h2>

Caso tenha algum resquício de alguma instalação do MySQL WorkBench, realize o comando:

```
sudo apt remove --purge mysql-workbench*
```
Instalando a dependência do programa:

```
sudo apt install libgtkmm-3.0-1v5
```
Instalando o MySQL WorkBench:

```
sudo apt install mysql-workbench*
```
Entre no MySQL WorkBench e depois edite a conexão. Troque o nome do usuário (username) root para o seu_usuario. Feche o programa e depois entre novamente. Digite a sua senha e o MySQL WorkBench estará funcionando normalmente.

#MYSQL BÁSICOS


<h4>CREATE DATABASES</h4>

```sql
CREATE DATABASE meu_banco
default character set utf8
default collate utf8_general_ci;
```

<h4>SHOW DATABASES</h4>

```sql
SHOW DATABASES;

+--------------------+
| Database           |
+--------------------+
| information_schema |
| crudaplication     |
| formulariopdi      |
| mysql              |
| performance_schema |
| sys                |
| testando           |
+--------------------+

```

<h4>CREATE TABLE</h4>

Antes de criar uma tabela ou realizar qualquer operação, é necessário selecionar o banco de dados que vai ser usado:
```sql
USE meu_banco;
```
```
CREATE TABLE `clientes` (
`idCliente` mediumint(8) unsigned NOT NULL auto_increment,
`nomeEmpresa` varchar(255),
`nomeDiretor` varchar(255) default NULL,
`numEmpregados` mediumint default NULL,
PRIMARY KEY (`idCliente`)

) AUTO_INCREMENT=1;
```

<h4>SHOW TABLES</h4>

Sempre que quiser usar o SHOW tables deve selecionar o banco de dados primeiro. 

```sql
SHOW tables;

+--------------------+
| Tables_in_testando |
+--------------------+
| clientes           |
+--------------------+

```

<h4>DESCRIBE</h4>

```sql
DESC clientes;
```

```sql
DESCRIBE clientes;

+---------------+-----------------------+------+-----+---------+----------------+
| Field         | Type                  | Null | Key | Default | Extra          |
+---------------+-----------------------+------+-----+---------+----------------+
| idCliente     | mediumint(8) unsigned | NO   | PRI | NULL    | auto_increment |
| nomeEmpresa   | varchar(255)          | YES  |     | NULL    |                |
| nomeDiretor   | varchar(255)          | YES  |     | NULL    |                |
| numEmpregados | mediumint(9)          | YES  |     | NULL    |                |
+---------------+-----------------------+------+-----+---------+----------------+

```

<h4>INSERT INTO</h4>

```sql
INSERT INTO `clientes` (`nomeEmpresa`,`nomeDiretor`,`numEmpregados`) VALUES ("Malesuada Inc.","Johnny Pedd",4847);
```
Note que no exemplo não tem o campo idCliente, pois foi criado com o parâmetro auto_increment. Seu preenchimento é automático.

<h4>SELECT</h4>

```sql
SELECT * FROM clientes;
```

Para ver colunas selecionadas:

```sql
SELECT nomeDiretor FROM clientes;

+-------------------+
| nomeDiretor       |
+-------------------+
| Macaulay Bulkin   |
| Jonathan Domingos |
| Leda Grasiele     |
+-------------------+

```

<h4>DELETE</h4>

```sql
DELETE FROM clientes WHERE nomeDiretor = 'Jonathan Domingos';
```
Neste caso, deletei todos os registros ligado ao Jonathan. Minha tabela ficou assim:

```sql

SELECT * FROM clientes;


+-----------+-------------+-----------------+---------------+
| idCliente | nomeEmpresa | nomeDiretor     | numEmpregados |
+-----------+-------------+-----------------+---------------+
|         1 | In Company  | Macaulay Bulkin |          4440 |
|         3 | MinasSA     | Leda Grasiele   |           340 |
+-----------+-------------+-----------------+---------------+
```

Cuidado: A comando DELETE acima deletará todos registros relacionados a Jonathan, caso queira deletar apenas uma única linha, identificar pelo id:

```sql
DELETE FROM clientes WHERE idCliente = 7;
```

<h4>DROP TABLE</h4>

Eliminar uma tabela:

```sql
DROP TABLE nome_da_tabela;
```

<h4>DROP DATABASE</h4>

Elimina um banco de dados:

```sql
DROP DATABASE nome_do_banco;
```

<h4>TRUNCATE</h4>

Para limpar uma tabela, use o comando TRUNCATE. Internamente, ele remove a tabela primeiro e, depois, a recria com a mesma estrutura – só que sem os dados. Se houver um contador AUTO_INCREMENT, na tabela em questão, ele é zerado e recolocado. Veja como funciona:

```sql
TRUNCATE TABLE nome_da_tabela;
```

<h4>UPDATE</h4>

```sql
UPDATE clientes SET numEmpregados=1999 WHERE idCliente = 1;
```


#MYSQL EXEMPLOS


<h4>CREATE TABLE</h4>

```sql
CREATE TABLE `pessoas` (
`id` int NOT NULL AUTO_INCREMENT,
`nome` varchar(30) NOT NULL,
`nascimento` date,
`sexo` enum('M','F'),
`peso` decimal (5,2),
`altura` decimal (3,2),
`nacionalidade` varchar(20) DEFAULT 'Brasil',
PRIMARY KEY (id)
) DEFAULT CHARSET = utf8;
```
Outro Exemplo:

```sql
CREATE TABLE IF NOT EXISTS `cursos` (
`nome` varchar(30) NOT NULL UNIQUE,
`descricao` text,
`carga` int UNSIGNED,
`totaulas` int UNSIGNED,
`ano` year DEFAULT '2016',
) DEFAULT CHARSET = utf8;
```



<h4>INSERT INTO</h4>

```sql
INSERT INTO `pessoas` (`nome`, `nascimento`, `sexo`,`peso`, `altura`, `nacionalidade`) VALUES ('Godofredo', '1984-01-02', 'M', '78.5', '1.83', 'Brasil');

INSERT INTO `pessoas` (`id`, `nome`, `nascimento`, `sexo`,`peso`, `altura`, `nacionalidade`) VALUES (DEFAULT, 'Creuza', '1999-01-02', 'F', '78.5', '1.83', 'Argentina'), 
(DEFAULT, 'Carlos', '1999-01-02', 'M', '80.5', '1.83', 'Uruguai');

```
<h4>SELECT ALL</h4>

```sql
SELECT * FROM pessoas;

+----+-----------+------------+------+-------+--------+---------------+
| id | nome      | nascimento | sexo | peso  | altura | nacionalidade |
+----+-----------+------------+------+-------+--------+---------------+
|  1 | Godofredo | 1984-01-02 | M    | 78.50 |   1.83 | Brasil        |
|  2 | Maria     | 1999-01-02 | F    | 78.50 |   1.83 | Portugal      |
|  3 | Creuza    | 1999-01-02 | F    | 78.50 |   1.83 | Argentina     |
|  4 | Carlos    | 1999-01-02 | M    | 80.50 |   1.83 | Uruguai       |
+----+-----------+------------+------+-------+--------+---------------+

```
<h4>DESCRIBE</h4>

```sql
DESC pessoas;

+---------------+---------------+------+-----+---------+----------------+
| Field         | Type          | Null | Key | Default | Extra          |
+---------------+---------------+------+-----+---------+----------------+
| id            | int(11)       | NO   | PRI | NULL    | auto_increment |
| nome          | varchar(30)   | NO   |     | NULL    |                |
| nascimento    | date          | YES  |     | NULL    |                |
| sexo          | enum('M','F') | YES  |     | NULL    |                |
| peso          | decimal(5,2)  | YES  |     | NULL    |                |
| altura        | decimal(3,2)  | YES  |     | NULL    |                |
| nacionalidade | varchar(20)   | YES  |     | Brasil  |                |
+---------------+---------------+------+-----+---------+----------------+

```

<h4>ADD COLUMN</h4>

Adicionar uma coluna em minha tabela:

```sql
ALTER TABLE pessoas ADD COLUMN profissao varchar(10);
```
```sql
DESC pessoas;
+---------------+---------------+------+-----+---------+----------------+
| Field         | Type          | Null | Key | Default | Extra          |
+---------------+---------------+------+-----+---------+----------------+
| id            | int(11)       | NO   | PRI | NULL    | auto_increment |
| nome          | varchar(30)   | NO   |     | NULL    |                |
| nascimento    | date          | YES  |     | NULL    |                |
| sexo          | enum('M','F') | YES  |     | NULL    |                |
| peso          | decimal(5,2)  | YES  |     | NULL    |                |
| altura        | decimal(3,2)  | YES  |     | NULL    |                |
| nacionalidade | varchar(20)   | YES  |     | Brasil  |                |
| profissao     | varchar(10)   | YES  |     | NULL    |                |
+---------------+---------------+------+-----+---------+----------------+
```

<h4>ADD COLUMN 2</h4>

Adicionar uma coluna em minha tabela, escolhendo a posição:

```sql
ALTER TABLE pessoas ADD COLUMN profissao varchar(10) after nome;
```

<h4>ADD COLUMN 3</h4>

Adicionar uma coluna em minha tabela, escolhendo a primeira posição:

```sql
ALTER TABLE pessoas ADD COLUMN código INT first;
```

<h4>MODIFY COLUMN</h4>
Modificando o tipo primitivo e as constraints. No caso abaixo troquei varchar(10) por varchar(30).

```sql
ALTER TABLE pessoas MODIFY COLUMN profissao varchar(20) not null default '';
```

<h4>CHANGE COLUMN</h4>
Renomear a coluna.

```sql
ALTER TABLE pessoas CHANGE COLUMN profissao prof varchar(20) not null default '';
```
OBS: o uso do not null defaul '' é para permitir ter uma coluna not null. 

<h4>RENAME TO</h4>
Renomear a tabela.

```sql
ALTER TABLE pessoas RENAME TO pessoal;
```

<h4>ADD PRIMARY KEY</h4>

```sql
ALTER TABLE cursos ADD COLUMN id INT first;

ALTER TABLE cursos ADD PRIMARY KEY (id);
```


<h4>DROP COLUMN</h4>

Apagar uma coluna em minha tabela:

```sql
ALTER TABLE pessoas DROP COLUMN profissao;
```

------------------------------------------------------------------------
<br>
<br>


<h4>TUTORIAL UNICAMP</h4>

```sql
CREATE TABLE taxi (
placa VARCHAR (7) NOT NULL,
marca VARCHAR (30) NOT NULL,
modelo VARCHAR (30) NOT NULL,
ano INTEGER,
licenca VARCHAR (9),
PRIMARY KEY (placa)
);
```

```sql

CREATE TABLE cliente (
cliId VARCHAR (4) NOT NULL,
nome VARCHAR (80) NOT NULL,
cpf VARCHAR (14) NOT NULL,
PRIMARY KEY (cliId)
);
```



```sql
CREATE TABLE corrida (
cliId VARCHAR (4) NOT NULL,
placa VARCHAR (7) NOT NULL,
dataPedido DATE NOT NULL,
PRIMARY KEY (cliId, placa, dataPedido),
FOREIGN KEY (cliId)
    REFERENCES cliente (cliId)
        ON DELETE NO ACTION
        ON UPDATE NO ACTION,
FOREIGN KEY (placa)
    REFERENCES taxi (placa)
        ON DELETE NO ACTION
        ON UPDATE NO ACTION
);
```






OBS: FOREIHN KEY = Chave estrangeira que aponta para a chave primária de outro campo.

Ações em relação a tabela a qual estou referenciando, ou seja, a tabela que possui a primary key. 

    NO ACTION = impede a ação na tabela mestre (tabela_ref)
    CASCADE = propaga a ação da tabela mestre (Apaga tudo ou altera tudo)
    SET NULL = valores de referências alterados para nulo.
    SET DEFAULT = valores de referências alterados para default. 

