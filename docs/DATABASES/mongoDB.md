# MONGO_DB

MongoDB é um banco de dados orientado a documentos, é de código aberto, gratuito e de alta performance. Foi escrito na linguagem de programação C++, o que o torna multiplataforma. Classificado como um programa de banco de dados NoSQL, o MongoDB usa documentos semelhantes a JSON com esquemas. É desenvolvido pela MongoDB Inc. e publicado sob uma combinação da GNU Affero General Public License e Licença Apache. Suas características permitem com que as aplicações modelem informações de modo muito mais natural, pois os dados podem ser aninhados em hierarquias complexas e continuar a ser indexáveis e fáceis de buscar.

<button onclick="window.open('https://www.mongodb.com/');">MONGO - LOGIN</button>
<button onclick="window.open('https://cloud.mongodb.com/user#/atlas/login');">MONGO - HOME</button>


Acesse meu github para consultar a documentação completa, lá você encontrará, além desta documentação, alguns exemplos de python funcional utilizando o mongoDB e a pymongo. 

<button onclick="window.open('https://github.com/Jonathan-geo');">GITHUB</button>

OBS: Para esta documentação foi utilizado um cluster no mongodb cloud.

### Install

```bash

#  No terminal 

$ python -m pip install pymongo
$ python -m pip install pymongo[srv]

```


### Import

```python
from pymongo import MongoClient
from pprint import pprint
```
OBS: A biblioteca pprint foi utilizada para que o outputs fossem estilizados semelhantes formato json. 

### Connect

```python
connection = MongoClient("mongodb+srv://login:senha@cluster0-5ueib.mongodb.net/test?retryWrites=true&w=majority")
```
### Create - DB

Criando o banco de dados "moonlightDB" e instanciando uma variavel de mesmo nome a ele.

```python
#Estabelecendo a conexão 
connection = MongoClient("mongodb+srv://login:senha@cluster0-5ueib.mongodb.net/test?retryWrites=true&w=majority")

#Criando um DB
moonlightDB = connection["moonlightDB"]
```

### Create - Collection

Criando uma coleção (Tabela) "heroes" e instanciando uma variavel de mesmo nome a esta coleção.
 
```python

#Estabelecendo a conexão 
connection = MongoClient("mongodb+srv://login:senha@cluster0-5ueib.mongodb.net/test?retryWrites=true&w=majority")

#Criando um DB
moonlightDB = connection["moonlightDB"]

#Criando uma colection
heroes = moonlightDB["heroes"]

```

OBS: No MongoDB, um banco de dados e uma coleção não é criada até obter conteúdo! 
O MongoDB aguarda até que você tenha inserido um documento antes que ele realmente crie a coleção.


### Create - document

Criando um documento (Paladino) e inserindo ele em uma coleção (heroes):

```python

#Estabelecendo a conexão 
connection = MongoClient("mongodb+srv://login:senha@cluster0-5ueib.mongodb.net/test?retryWrites=true&w=majority")

#Criando um DB
moonlightDB = connection["moonlightDB"]

#Criando uma colection
heroes = moonlightDB["heroes"]

#Criando um documento
Paladino = { "name": "Jonathan", 
            "Classe": "paladino",
            "força": 21, 
            "defesa": 19, 
            "arma": "espada longa",
            "poder1": "ataque divino",
            "poder2": "cura pelas mãos" }

inserColeçao = heroes.insert_one(Paladino)
print(inserColeçao.inserted_id)
```


**Criando vários documentos e inserindo eles em uma coleção (Tabela):**

```python
variosHerois = [{ "name": "Leda", 
                "Classe": "mago de fogo",
                "força": 18, 
                "defesa": 13, 
                "arma": "cajado",
                "poder1": "bola de fogo",
                "poder2": "chuva de meteoro" },
                
                { "name": "Anny", 
                "Classe": "animal",
                "força": 11, 
                "defesa": 15, 
                "arma": "guarra",
                "poder1": "furtividade",
                "poder2": "guarras afiadas" },

                { "name": "Nick", 
                "Classe": "animal",
                "força": 15, 
                "defesa": 14, 
                "arma": "mordida",
                "poder1": "velocidade",
                "poder2": "mordida frontal" },
]

inserindoTudo = heroes.insert_many(variosHerois)

print(inserindoTudo.inserted_ids)
```

**Criando um documento com ID. Lembre-se, dois documentos NÃO podem ter o mesmo ID.**

```python
# Paladino = { "_id": 1,
#             "name": "Jonathan",
#             "Classe": "paladino",
#             "força": 24,
#             "defesa": 19,
#             "arma": "espada longa",
#             "poder1": "ataque divino",
#             "poder2": "cura pelas mãos" }

# inserColeçao = heroes.insert_one(Paladino)
# print(inserColeçao.inserted_id)
```

**Posso criar documentos com mais {chave: valor} em uma mesma colection.**

```python
Paladino = { "_id": 2,
            "name": "Trevor",
            "Classe": "Knight",
            "força": 24,
            "defesa": 19,
            "arma": "espada longa",
            "poder1": "ataque divino",
            "poder2": "cura pelas mãos",
            "poder3": "Espada da noite" }

inserColeçao = heroes.insert_one(Paladino)
print(inserColeçao.inserted_id)
```

### Select - Data Base

Listando e buscando banco de dados em minha conta mongoDB. Lembrando que minha conexão está com o nome de "coonection"

```python
pprint (connection.list_database_names())
```

```python
dblist = connection.list_database_names()
if "moonlightDB" in dblist:
  print("O banco de dados existe.")
else:
    print ("O banco de dados não existe.")
```
### Select - Collection

Listando e buscando coleções (Tabelas) no meu banco de dados "moonlight".

```python
pprint (moonlightDB.list_collection_names())
```

```python
collist = moonlightDB.list_collection_names()
if "heroes" in collist:
  print("A coleção existe.")
```

Contando o número de documentos dentro da minha colection

```python
pprint(heroes.count_documents({}))
```
### Select - Docment

Selecionando o primeiro documento da coleção (heroes)

```python
pprint(heroes.find_one())
```


Selecionando um documento por {chave: Valor}:

```python
pprint(heroes.find_one({"arma": "mordida"}))
```


Selecionando todos os documentos da minha coleção:

```python
for personagens in heroes.find():
    pprint(personagens)
```

Selecionando todos os documentos da minha coleção (Número limitado)

```python
selLimite = heroes.find().limit(5)
```

```python
for x in selLimite:
  pprint(x)
```

Selecionando todos os documentos que possuem uma mesma {chave:valor} selecionada:

```python
for animais in heroes.find({"classe": "animal"}):
    pprint(animais)
```


Selecionando o nome e a arma de todos os documentos.
Só posso atribuir falso (0) para o id, pois ele é o unico que aparece mesmo quando não mensionado. 
 
```python
for nomes in heroes.find({},{ "_id": 0, "name": 1, "arma": 1 }):
  pprint(nomes)


#Neste caso o ID, aparecerá também. 
for armas in heroes.find({},{ "name": 1, "arma": 1 }):
  pprint(armas)

#Neste caso o id não aparecerá.
for classes in heroes.find({},{ "_id": 0, "classe": 1, "name": 1, "arma": 1 }):
  pprint(classes)

```


Instanciando uma busca. 

```python
cajado = { "arma": "cajado" }
busca = heroes.find(cajado)

for x in busca:
  pprint(x)
```


Buscar os documento em que o valor da chave nome comessem com a 
letra T ou posterior no alfabeto. (T, U, V, ...). Lembrando que os nomes estão em maiúscula.
A mesma busca pode ser feita por regex: letraJ = { "name": { "$regex": "^S" } }

```python

letraJ = { "name": { "$gt": "T" } }
busca = heroes.find(letraJ)

for x in busca:
  pprint(x)



# >>>>>> Selecionando os documentos por ordem alfabética (nome):
nomePorOredem = heroes.find().sort("name")

for x in nomePorOredem:
  pprint(x)


# >>>>>> Selecionando por ordem decrescente. Para o caso de ordem crescente substituir o -1 por 1.
ordemDecrescente = heroes.find().sort("name", -1)

for x in ordemDecrescente:
  pprint(x)
```
### Delete - Document

Deleta o primeiro documento com o nome selecionado 

```python
delNome = { "name": "Jonathan" }

heroes.delete_one(delNome)
```
Deletando vários documentos e retornando o número de documentos deletados. 

```python
delVarios = { "name": {"$regex": "^N"} }
deletados = heroes.delete_many(delVarios)
print(deletados.deleted_count)
```

Deletando todos os documentos de uma coleção:

```python
delTodos = heroes.delete_many({})
print(delTodos.deleted_count)
```

### Delete - Collection

```python
heores.drop()
```

### Update - Values

Alterando valores de um documento:

```python
valorAntigo = { "name": "Trevor" }
novoValor = { "$set": { "name": "Belmont" } }
heroes.update_one(valorAntigo, novoValor)
```

Referências:

- https://pt.wikipedia.org/wiki/MongoDB
- https://docs.mongodb.com/manual/reference/method/db.collection.updateOne/
- https://codehandbook.org/pymongo-tutorial-crud-operation-mongodb/
- https://www.w3schools.com/python/python_mongodb_getstarted.asp
- https://imasters.com.br/banco-de-dados/mongodb-para-iniciantes-em-nosql
- https://api.mongodb.com/python/current/tutorial.html
- https://pypi.org/project/pymongo/