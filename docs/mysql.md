#MySQL 

O MySQL é um sistema gerenciador de banco de dados relacional de código aberto. O serviço utiliza a linguagem SQL (Structured Query Language – Linguagem de Consulta Estruturada), que é a linguagem mais popular para inserir, acessar e gerenciar o conteúdo armazenado num banco de dados. O MySQL é um produto regido pela licença GPL (General Public License). Portanto, é "parcialmente" Open Source.
Nesta documentação utilizarei o LAMP, um acrônimo para Linux, Apache, MySQL e Perl/PHP/Python. Nesse conjunto de aplicações, inclui-se, respectivamente, um sistema operacional, um servidor web, um sistema gerenciador de banco de dados e uma linguagem de programação.

-----------------------------------------------------------------

#Instalação

OBS: O sistema operacional utilizado é o Linux Ubuntu. 
Executar em ordem, no terminal:

**Instalando o Apache**


```

sudo apt update 

sudo apt upgrade -y

sudo apt install -y apache2

```


Para testar se o Apache está funcionando corretamente, devemos digitar localhost na barra de endereços do navegador de sua preferência.


**Instalando o PHP**


```
sudo apt install -y php php-cli php-common php-gd php-mbstring php-intl php-xml php-zip php-pear libapache2-mod-php
```
**Testando o PHP**


```
echo “<?php phpinfo(); ?>” | sudo tee /var/www/html/test.php | sudo service apache2 restart
```
Para testar o PHP no navegador, digite na página de endereços: 

>localhost/test.php


**Instalando o MySQL**

```
sudo apt install -y mysql-server mysql-client php-mysql
```

**Acessar o MySQL no Terminal**

```
sudo mysql
```

------------------------------------------------------------------

##Configuração 

**Criar novo usuário**

```
sudo mysql 
#Ou somente mysql(depende de seu acesso)


CREATE USER 'seu_usuario'@'localhost' IDENTIFIED BY 'sua_senha';
GRANT ALL PRIVILEGES ON *.* TO 'seu_usuario'@'localhost' WITH GRANT OPTION;
```


**Entrando com o usuário criado**


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

--------------------------------------------------------------------

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

Cuidado: A comando DELETE acima deletará todos registros relacionados a Jonathan. Caso queira deletar apenas uma única linha, identificar pelo id:

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


#SQL - UNICAMP

Este cheat Sheet foi elaborado com o intuito de ser meu material de rápida consulta sql. Todos os códigos descritos aqui podem ser encontrados no material do professor <a href="https://www.ic.unicamp.br/~santanch/" target="_blank">André Santanchè</a> disponibilizados em seu site. Inclusive, lá você encontrará  o material completo disponível para download.

**Algumas Observações:**

1. FOREIHN KEY = Chave estrangeira que aponta para a chave primária de outro campo.Ações em relação à tabela a qual estou referenciando, ou seja, a tabela que possui a primary key.
2. NO ACTION = impede a ação na tabela mestre (tabela_ref)
3. CASCADE = propaga a ação da tabela mestre (Apaga tudo ou altera tudo)
4. SET NULL = valores de referências alterados para nulo.
5. SET DEFAULT = valores de referências alterados para default.


##CREATE TABLE

```sql
CREATE TABLE Taxi (
  Placa VARCHAR(7) NOT NULL,
  Marca VARCHAR(30) NOT NULL,
  Modelo VARCHAR(30) NOT NULL,
  AnoFab INTEGER,
  Licenca VARCHAR(9),
  PRIMARY KEY(Placa)
);

CREATE TABLE Cliente (
  CliId VARCHAR(4) NOT NULL,
  Nome VARCHAR(80) NOT NULL,
  CPF VARCHAR(14) NOT NULL,
  PRIMARY KEY(CliId)
);

CREATE TABLE Corrida (
  CliId VARCHAR(4) NOT NULL,
  Placa VARCHAR(7) NOT NULL,
  DataPedido DATE NOT NULL,
  PRIMARY KEY(CliId, Placa, DataPedido),
  FOREIGN KEY(CliId)
    REFERENCES Cliente(CliId)
      ON DELETE NO ACTION
      ON UPDATE NO ACTION,
  FOREIGN KEY(Placa)
    REFERENCES Taxi(Placa)
      ON DELETE NO ACTION
      ON UPDATE NO ACTION
);

CREATE TABLE Motorista (
  CNH VARCHAR(6) NOT NULL,
  Nome VARCHAR(80) NOT NULL,
  CNHValid INTEGER,
  Placa VARCHAR(7) NOT NULL,
  PRIMARY KEY(CNH),
  FOREIGN KEY(Placa)
    REFERENCES Taxi(Placa)
      ON DELETE NO ACTION
      ON UPDATE NO ACTION
);

CREATE TABLE Zona (
  Zona VARCHAR(40) NOT NULL,
  PRIMARY KEY(Zona)
);

CREATE TABLE Fila (
   Zona VARCHAR(40) NOT NULL,
   CNH VARCHAR(6) NOT NULL,
   DataHoraIn TIMESTAMP,
   DataHoraOut TIMESTAMP,
   KmIn INTEGER,
   PRIMARY KEY (Zona, CNH),
   FOREIGN KEY(Zona)
     REFERENCES Zona(Zona)
       ON DELETE NO ACTION
       ON UPDATE NO ACTION,
   FOREIGN KEY(CNH)
     REFERENCES Motorista(CNH)
       ON DELETE NO ACTION
       ON UPDATE NO ACTION
);

```
##INSERT INTO

```sql
INSERT INTO Cliente VALUES ('1532', 'Asdr�bal', '448.754.253-65');
INSERT INTO Taxi VALUES ('DAE6534', 'Ford', 'Fiesta', 1999, 'MN572345');
INSERT INTO Corrida VALUES ('1755', 'DAE6534', '2003-02-15');
INSERT INTO Motorista VALUES ('657483', 'Asdrubal', 1, 'DXF5263');
INSERT INTO Zona VALUES ('Unicamp');
INSERT INTO Fila VALUES ('Bar�o Geraldo', '567892', '2002-06-05 09:00:00', '2002-06-05 09:30:00', 4630);
```
##SELECT

```sql

SELECT * FROM Taxi;

SELECT Marca, Modelo FROM Taxi;

SELECT * FROM Taxi WHERE AnoFab > 2000;

-- Placas que comecem com DK
SELECT * FROM Taxi WHERE placa LIKE 'DK%';
'''
%  (encontra qualquer cadeia com 0 a n caracteres).
_  (encontra exatamente um caractere (qualquer)).
=  (caractere de escape)
'''
-- Placas com '7' na penultima posicao
SELECT * FROM Taxi WHERE placa LIKE '%7_';

-- Produto cartesiano Cliente x Corrida
SELECT Cliente.CliId, Cliente.Nome, Corrida.CliId, Corrida.Placa, Corrida.DataPedido
       FROM Cliente, Corrida;

-- Join (1) Cliente x Corrida
SELECT Cliente.CliId, Cliente.Nome, Corrida.CliId, Corrida.Placa, Corrida.DataPedido
       FROM Cliente, Corrida
       WHERE Cliente.CliId = Corrida.CliId;

-- Clientes (id e nome) e respectivas corridas (placa e data do pedido)
SELECT Cliente.CliId, Cliente.Nome, Corrida.Placa, Corrida.DataPedido
       FROM Cliente, Corrida
       WHERE Cliente.CliId = Corrida.CliId;

-- Alias (apelido) com o AS
SELECT Cl.CliId, Cl.Nome, Co.Placa, Co.DataPedido
       FROM Cliente AS Cl, Corrida AS Co
       WHERE Cl.CliId = Co.CliId;

-- Alias sem o AS
SELECT Cl.CliId, Cl.Nome, Co.Placa, Co.DataPedido
       FROM Cliente Cl, Corrida Co
       WHERE Cl.CliId = Co.CliId;

-- Alias dos campos com o AS
SELECT Cl.CliId AS id_cliente, Cl.Nome AS nome_cliente, Co.Placa AS placa, Co.DataPedido AS data_pedido
       FROM Cliente Cl, Corrida Co
       WHERE Cl.CliId = Co.CliId;       

-- Alias dos campos sem o AS
SELECT Cl.CliId id_cliente, Cl.Nome nome_cliente, Co.Placa placa, Co.DataPedido data_pedido
       FROM Cliente Cl, Corrida Co
       WHERE Cl.CliId = Co.CliId;       

-- Modelo de taxi para cada corrida
SELECT Co.DataPedido, Co.Placa, T.Modelo
       FROM Corrida Co, Taxi T
       WHERE Co.Placa = T.Placa;

-- Modelos de taxi tomados por cada cliente
-- (estagio 1)
SELECT Cl.Nome, Co.DataPedido, Co.Placa, T.Modelo
       FROM Cliente Cl, Corrida Co, Taxi T
       WHERE Cl.CliId = Co.CliId AND Co.Placa = T.Placa;
-- (estagio 2) - mais preciso para esta questão
SELECT DISTINCT Cl.Nome, T.Modelo
       FROM Cliente Cl, Corrida Co, Taxi T
       WHERE Cl.CliId = Co.CliId AND Co.Placa = T.Placa;

'''
DISTINCT (Não retorna tuplas duplicadas(iguais))
'''


-- CNH e Nome dos motoristas que jah estiveram e estao na fila
SELECT DISTINCT M.CNH, M.Nome
       FROM Motorista M, Fila F
       WHERE M.CNH = F.CNH;

-- CNH e Nome dos motoristas que estao na fila
SELECT M.CNH, M.Nome
       FROM Motorista M, Fila F
       WHERE M.CNH = F.CNH AND DataHoraIn = DataHoraOut;

-- Placa dos taxis que jah estiveram e estao na fila
SELECT M.Placa
       FROM Motorista M, Fila F
       WHERE M.CNH = F.CNH;

-- Data/Hora entrada, nome e modelo dos taxis
-- que jah estiveram e estao na fila
SELECT Fila.DataHoraIn, Motorista.Nome, Taxi.Modelo
       FROM Fila, Motorista, Taxi
       WHERE Motorista.CNH = Fila.CNH AND
             Motorista.Placa = Taxi.Placa;

-- Marca e modelo dos taxis que jah estiveram e estao na fila
SELECT T.Marca, T.Modelo
       FROM Taxi T, Motorista M, Fila F
       WHERE T.Placa = M.Placa AND
             M.CNH = F.CNH;

-- Marca e modelo dos taxis que jah estiveram e estao na fila
-- (sem repeticao)
SELECT DISTINCT T.Marca, T.Modelo
       FROM Taxi T, Motorista M, Fila F
       WHERE T.Placa = M.Placa AND
             M.CNH = F.CNH;

-- Nome dos taxistas que jah estiveram e estao na fila
-- em ordem alfabetica
SELECT DISTINCT M.Nome
       FROM Motorista M, Fila F
       WHERE M.CNH = F.CNH
       ORDER BY M.Nome;             

-- Operadores avancados de comparacao
-- ----------------------------------       

-- Motoristas cujo nome comeca com a letra A
SELECT * FROM Motorista WHERE nome LIKE 'A%';

-- Motoristas com 'a' na penultima letra
SELECT * FROM Motorista WHERE nome LIKE '%a_';

-- Nome dos motoristas que jah estiveram e estao na fila
-- e cujo nome inicia com A
SELECT DISTINCT M.Nome
       FROM Motorista M, Fila F
       WHERE M.CNH = F.CNH AND
             M.Nome LIKE 'A%';

-- CNH dos motoristas que jah estiveram ou estao
-- nas filas das zonas Taquaral ou Unicamp
SELECT DISTINCT cnh, zona FROM Fila WHERE zona
       IN ('Taquaral', 'Unicamp');

-- CNH dos motoristas que nunca estiveram nem estao
-- nas filas das zonas Taquaral ou Unicamp
SELECT DISTINCT cnh, zona FROM Fila WHERE zona
       NOT IN ('Taquaral', 'Unicamp');

-- Entradas na fila entre 05 e 06/06/2002
SELECT * FROM Fila WHERE DataHoraIn
       BETWEEN '2002-06-05 00:00:00' AND '2002-06-06 23:59:59';             

-- Agregacao
-- ---------

-- Quais as zonas que tem ou tiveram algum taxi na fila (com repeticao)
SELECT Fila.zona FROM Fila;

-- Quais as zonas que tem ou tiveram algum taxi na fila (sem repeticao)
SELECT DISTINCT Fila.Zona FROM Fila;

-- Quais as zonas que tem ou tiveram algum taxi na fila (sem repeticao)
SELECT Zona
       FROM Fila
       GROUP BY Zona;

-- Para cada zona atendida, quantos taxis jah passaram pela fila
-- (contando com os que estao atualmente)
SELECT zona, COUNT(*)
       FROM Fila
       GROUP BY zona;

-- Quantos entradas de taxi tem/tiveram cada fila das zonas atendidas
-- (coluna COUNT com nome)       
SELECT Zona, COUNT(*) Quantidade
       FROM Fila
       GROUP BY Zona;

-- Marca e modelo dos taxis que estao/estiveram
-- em alguma fila com quantidades
SELECT T.Marca, T.Modelo, COUNT(*)
       FROM Taxi T, Motorista M, Fila F
       WHERE T.Placa = M.Placa AND
             M.CNH = F.CNH
       GROUP BY T.Marca, T.Modelo;

-- Zona, quilometragem e data/hora de cada taxi que esta/esteve em uma fila
SELECT Zona, KmIn, DataHoraIn FROM Fila;

-- Menor quilometragem de entrada em cada zona
SELECT Zona, MIN(KmIn) FROM Fila GROUP BY Zona;

-- Zona, data e hora de entrada do proximo taxi a ser chamado em cada zona
-- (menor data/hora entrada)
SELECT Zona, MIN(DataHoraIn) FROM Fila
       WHERE DataHoraIn = DataHoraOut
       GROUP BY Zona;

-- Maior data/hora de entrada para cada zona
SELECT Zona, MAX(DataHoraIn) FROM Fila
       GROUP BY Zona;

-- Zona, menor km, media km, maior data/hora para cada zona
SELECT Zona, MIN(KmIn), AVG(KmIn), MAX(DataHoraIn) FROM Fila
       GROUP BY Zona;

-- Maior data/hora dentre os taxis de cada zona com km <= 5000       
SELECT Zona, MAX(DataHoraIn) FROM Fila
       WHERE KmIn <= 5000 GROUP BY Zona;

-- Maior data/hora apenas para zonas cuja maxima km <= 5000
SELECT Zona, MAX(DataHoraIn) FROM Fila GROUP BY Zona
       HAVING MAX(KmIn) <= 5000;

-- Zonas que tem/tiveram mais de um taxi na fila
SELECT Zona FROM Fila GROUP BY Zona HAVING COUNT(*)>1;

-- Visoes
-- ------

-- Para cada zona atendida, quantos taxis passaram pela fila
CREATE VIEW QuantidadeFila AS
SELECT zona, COUNT(*) quantidade
       FROM Fila
       GROUP BY zona;

SELECT * FROM QuantidadeFila;

DROP VIEW QuantidadeFila;
```
##UPDATE

```sql
-- atualize a hora de entrada para o taxi cujo motorista tem CNH 452635
UPDATE Fila
       SET DataHoraOut = '2002-06-02 10:00:00'
       WHERE CNH='452635' AND DataHoraIn='2002-06-02 08:00:00';

```
##JOIN

```sql

-- Taxis e respectivas corridas (para taxis que fizeram corrida)
SELECT Tx.placa, Co.cliid
       FROM Taxi Tx, Corrida Co
       WHERE Tx.placa = Co.placa;

-- Taxis e respectivas corridas (para taxis que fizeram corrida)
SELECT Tx.placa, Co.cliid
       FROM Taxi Tx JOIN Corrida Co
            ON Tx.placa = Co.placa;       

-- Taxis e respectivas corridas (para taxis que fizeram corrida)
SELECT Tx.placa, Co.cliid
       FROM Taxi Tx NATURAL JOIN Corrida Co;

-- Taxis e respectivas corridas (para todos os taxis)
SELECT Tx.placa, Co.cliid
       FROM Taxi Tx LEFT JOIN Corrida Co
            ON Tx.placa = Co.placa;

-- CNH de quem esta na fila e todas as zonas
SELECT F.cnh, Z.zona
       FROM Fila F RIGHT JOIN Zona Z
            ON F.zona = Z.zona;

SELECT C.cliid, M.placa, M.nome
       FROM Corrida C FULL JOIN Motorista M
            ON C.placa = M.placa;
```
##SELECT ANINHADO

```sql
SELECT * FROM Zona;

SELECT * FROM Fila;

-- Zonas que receberam algum taxi na fila (sem aninhamento)
SELECT DISTINCT Z.zona
       FROM Zona Z, Fila F
       WHERE Z.zona = F.zona;

-- Zonas que receberam algum taxi na fila (com aninhamento / IN)
SELECT Z.zona
       FROM Zona Z
       WHERE Z.zona IN (SELECT DISTINCT F.zona FROM Fila F);

-- Zonas que receberam algum taxi na fila (com aninhamento / EXISTS)
SELECT Z.zona
       FROM Zona Z
       WHERE EXISTS (SELECT * FROM Fila F WHERE F.zona = Z.zona);

-- Zonas que nao receberam algum taxi na fila (com aninhamento / NOT IN)
SELECT Z.zona
       FROM Zona Z
       WHERE Z.zona NOT IN (SELECT DISTINCT F.zona FROM Fila F);

-- Zonas que nao receberam algum taxi na fila (com aninhamento / NOT EXISTS)
SELECT Z.zona
       FROM Zona Z
       WHERE NOT EXISTS (SELECT * FROM Fila F WHERE F.zona = Z.zona);

-- Taxis modelo Fiesta
SELECT T.placa, T.modelo FROM Taxi T WHERE T.modelo = 'Fiesta';

-- Nome dos clientes que andaram nos taxis modelo Fiesta (sem aninhamento)
SELECT DISTINCT Cl.nome
       FROM Cliente Cl, Corrida Co, Taxi Tx
       WHERE Cl.cliid = Co.cliid AND Co.placa = Tx.placa AND
             Tx.modelo = 'Fiesta';

-- Nome dos clientes que andaram nos taxis modelo Fiesta (com aninhamento)
SELECT DISTINCT Cl.nome
       FROM Cliente Cl, Corrida Co
       WHERE Cl.cliid = Co.cliid AND
             Co.placa IN (SELECT Tx.placa FROM Taxi Tx
                                 WHERE Tx.modelo = 'Fiesta');

-- Nome dos clientes que andaram no taxi dirigido por Bonerges
SELECT DISTINCT Cl.nome
       FROM Cliente Cl, Corrida Co
       WHERE Cl.cliid = Co.cliid AND
             Co.placa = (SELECT Tx.placa FROM Taxi Tx, Motorista Mo
                                WHERE Tx.placa = Mo.placa AND
                                      Mo.nome = 'Bonerges');

-- Taxis que entraram na fila antes da primeira entrada de Alcebiades
SELECT Mo.placa, Fi.datahorain
       FROM Motorista Mo, Fila Fi
       WHERE Mo.cnh = Fi.cnh AND
             Fi.datahorain < (SELECT MIN(F.datahorain)
                                     FROM Motorista M, Fila F
                                     WHERE M.cnh = F.cnh AND
                                           M.nome = 'Alcebiades');                                      

-- Quem foi o primeiro motorista a entrar em qualquer uma das filas
SELECT Mo.nome, Fi.datahorain
       FROM Motorista Mo, Fila Fi
       WHERE Mo.cnh = Fi.cnh AND
             Fi.datahorain <= ALL (SELECT datahorain FROM Fila);

-- Quem nao foi o primeiro motorista a entrar em qualquer uma das filas
SELECT Mo.nome, Fi.datahorain
       FROM Motorista Mo, Fila Fi
       WHERE Mo.cnh = Fi.cnh AND
             Fi.datahorain > ANY (SELECT DataHoraIn FROM Fila);

```

##UNION

```sql
SELECT cliid, nome
       FROM Cliente;

SELECT cliid, nome
       FROM ClienteEmpresa;

-- Uniao de todos os clientes particulares e empresas       
SELECT cliid, nome
       FROM Cliente
UNION
SELECT cliid, nome
       FROM ClienteEmpresa;

-- UNION - INTERSECT - EXCEPT
```

##Exercício completo

```sql

CREATE TABLE Virus (
  virusid VARCHAR(5) NOT NULL,
  nome VARCHAR(100),
  PRIMARY KEY (virusid)
);

INSERT INTO Virus VALUES ('101', 'Quackrax');
INSERT INTO Virus VALUES ('102', 'X45');
INSERT INTO Virus VALUES ('301', 'Tubitubi');

CREATE TABLE Medicamento (
  medicamentoid VARCHAR(5) NOT NULL,
  nome VARCHAR(100),
  PRIMARY KEY (medicamentoid)
);

INSERT INTO Medicamento VALUES ('AspH', 'Aspargorim H');
INSERT INTO Medicamento VALUES ('Bon2', 'Bonergex Duplex');
INSERT INTO Medicamento VALUES ('AspM', 'Aspargorum M');
INSERT INTO Medicamento VALUES ('Bon3', 'Bonergex Triplex');
INSERT INTO Medicamento VALUES ('PinN', 'Pinicilina Ninja');

CREATE TABLE Trata (
  medicamentoid VARCHAR(5) NOT NULL,
  virusid VARCHAR(5) NOT NULL,
  PRIMARY KEY (medicamentoid, virusid),
  FOREIGN KEY(medicamentoid)
    REFERENCES Medicamento(medicamentoid)
      ON DELETE NO ACTION
      ON UPDATE NO ACTION,
  FOREIGN KEY(virusid)
    REFERENCES Virus(virusid)
      ON DELETE NO ACTION
      ON UPDATE NO ACTION
);

INSERT INTO Trata VALUES ('AspH', '101');
INSERT INTO Trata VALUES ('AspM', '101');
INSERT INTO Trata VALUES ('PinN', '101');
INSERT INTO Trata VALUES ('Bon2', '102');
INSERT INTO Trata VALUES ('Bon3', '102');
INSERT INTO Trata VALUES ('PinN', '102');
INSERT INTO Trata VALUES ('AspH', '301');
INSERT INTO Trata VALUES ('Bon2', '301');
INSERT INTO Trata VALUES ('Bon3', '301');


CREATE TABLE Sequencia (
  seqid VARCHAR(5) NOT NULL,
  virustratado VARCHAR(5) NOT NULL,
  PRIMARY KEY (seqid),
  FOREIGN KEY(virustratado)
    REFERENCES Virus(virusid)
      ON DELETE NO ACTION
      ON UPDATE NO ACTION
);

INSERT INTO Sequencia VALUES ('001', '101');
INSERT INTO Sequencia VALUES ('002', '101');
INSERT INTO Sequencia VALUES ('003', '101');
INSERT INTO Sequencia VALUES ('004', '301');
INSERT INTO Sequencia VALUES ('005', '301');
INSERT INTO Sequencia VALUES ('006', '102');

CREATE TABLE MedicamentosSequencia (
  seqid VARCHAR(5) NOT NULL,
  ordem INTEGER NOT NULL,
  medicamentoid VARCHAR(5) NOT NULL,
  melhora INTEGER NOT NULL,
  PRIMARY KEY (seqid, ordem),
  FOREIGN KEY(seqid)
    REFERENCES Sequencia(seqid)
      ON DELETE NO ACTION
      ON UPDATE NO ACTION,
  FOREIGN KEY(medicamentoid)
    REFERENCES Medicamento(medicamentoid)
      ON DELETE NO ACTION
      ON UPDATE NO ACTION
);

INSERT INTO MedicamentosSequencia VALUES ('001', 1, 'AspH', 2);
INSERT INTO MedicamentosSequencia VALUES ('001', 2, 'AspM', 1);
INSERT INTO MedicamentosSequencia VALUES ('001', 3, 'PinN', 1);
INSERT INTO MedicamentosSequencia VALUES ('002', 1, 'AspM', 3);
INSERT INTO MedicamentosSequencia VALUES ('002', 2, 'AspH', 3);
INSERT INTO MedicamentosSequencia VALUES ('002', 3, 'PinN', 1);
INSERT INTO MedicamentosSequencia VALUES ('003', 1, 'PinN', 5);
INSERT INTO MedicamentosSequencia VALUES ('003', 2, 'AspH', 3);
INSERT INTO MedicamentosSequencia VALUES ('003', 3, 'AspM', 1);
INSERT INTO MedicamentosSequencia VALUES ('004', 1, 'AspH', 1);
INSERT INTO MedicamentosSequencia VALUES ('004', 2, 'Bon2', 1);
INSERT INTO MedicamentosSequencia VALUES ('004', 3, 'Bon3', 2);
INSERT INTO MedicamentosSequencia VALUES ('005', 1, 'Bon2', 7);
INSERT INTO MedicamentosSequencia VALUES ('005', 2, 'AspH', 2);
INSERT INTO MedicamentosSequencia VALUES ('005', 3, 'Bon3', 2);
INSERT INTO MedicamentosSequencia VALUES ('006', 1, 'AspH', 1);
INSERT INTO MedicamentosSequencia VALUES ('006', 2, 'Bon2', 2);
INSERT INTO MedicamentosSequencia VALUES ('006', 3, 'PinN', 2);


-- relacao de sequencia de tratamentos (2 b)
SELECT V.nome, S.seqid, MS.ordem, M.nome, MS.melhora
       FROM Medicamento M, MedicamentosSequencia MS, Sequencia S, Virus V
       WHERE MS.medicamentoid = M.medicamentoid AND MS.seqid = S.seqid AND
             S.virustratado = V.virusid;

-- relacao de sequencia de tratamentos (2 c)
SELECT V.nome, S.seqid, MS.ordem, M.nome, MS.melhora
       FROM Medicamento M, MedicamentosSequencia MS, Sequencia S, Virus V
       WHERE MS.medicamentoid = M.medicamentoid AND MS.seqid = S.seqid AND
             S.virustratado = V.virusid
       ORDER BY S.seqid, MS.ordem;

-- total de melhora por sequencia de tratamento (2 d)
SELECT S.seqid, SUM(MS.melhora)
       FROM Medicamento M, MedicamentosSequencia MS, Sequencia S, Virus V
       WHERE MS.medicamentoid = M.medicamentoid AND MS.seqid = S.seqid AND
             S.virustratado = V.virusid
       GROUP BY S.seqid;

-- total de melhora por sequencia de tratamento (2 d)
SELECT S.virustratado virust, S.seqid seq, SUM(MS.melhora) totalmelhora
       FROM Medicamento M, MedicamentosSequencia MS, Sequencia S, Virus V
       WHERE MS.medicamentoid = M.medicamentoid AND MS.seqid = S.seqid AND
             S.virustratado = V.virusid
       GROUP BY S.virustratado, S.seqid;       

-- maior total de melhora por virus (2 e)
CREATE VIEW SomasSequencias AS
SELECT S.virustratado virust, SUM(MS.melhora) totalmelhora
       FROM MedicamentosSequencia MS, Sequencia S
       WHERE MS.seqid = S.seqid
       GROUP BY S.virustratado, S.seqid;       

SELECT * FROM SomasSequencias;       

SELECT virust, MAX(totalmelhora)
       FROM SomasSequencias
       GROUP BY virust;

DROP VIEW SomasSequencias;       

-- tratamentos com indice de melhora errado (acima de 10) (2 f)
SELECT S.seqid, S.virustratado
       FROM MedicamentosSequencia MS, Sequencia S, Virus V
       WHERE MS.seqid = S.seqid AND S.virustratado = V.virusid AND
             MS.melhora > 4
       GROUP BY S.seqid, S.virustratado;

-- tratamentos com indice de melhora errado (acima de 10) (2 g)
SELECT S.seqid, S.virustratado, SUM(MS.melhora)
       FROM MedicamentosSequencia MS, Sequencia S, Virus V
       WHERE MS.seqid = S.seqid AND S.virustratado = V.virusid
       GROUP BY S.seqid, S.virustratado
       HAVING SUM(MS.melhora) > 10;


 -- maior total de melhora por virus (2 e) usando inner
 SELECT Sq.virustratado virust, SUM(MSq.melhora) totalmelhora
        FROM MedicamentosSequencia MSq, Sequencia Sq
        WHERE MSq.seqid = Sq.seqid
        GROUP BY Sq.virustratado, Sq.seqid
        HAVING SUM(MSq.melhora) >= ALL
            (SELECT SUM(MS.melhora)
                    FROM MedicamentosSequencia MS, Sequencia S
                    WHERE MS.seqid = S.seqid AND
                          S.virustratado = Sq.virustratado
                    GROUP BY S.virustratado, S.seqid);
```








