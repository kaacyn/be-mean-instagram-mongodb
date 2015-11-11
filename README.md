###########
GERAL

Play List dba: https://www.youtube.com/playlist?list=PL77JVjKTJT2jyVllJeO3TZV9D5cfSvSjR
Padrão para envio de exercício: https://github.com/Webschool-io/be-mean-instagram/wiki/Exerc%C3%ADcios

###########
GERAL GIT
TUTORIAL GIT - https://www.youtube.com/watch?v=TReVFOxhh7E
GUIA RÀPIDO http://rogerdudler.github.io/git-guide/index.pt_BR.html
http://tableless.com.br/tudo-que-voce-queria-saber-sobre-git-e-github-mas-tinha-vergonha-de-perguntar/

################################
# Aula 1 - MONGO
################################

Página: https://github.com/Webschool-io/be-mean-instagram/blob/master/apostila/classes/mongodb/class-01.md
Vídeo: https://www.youtube.com/watch?v=leYxsEAL_yY&list=PL77JVjKTJT2jyVllJeO3TZV9D5cfSvSjR&index=9
Slide: https://docs.google.com/presentation/d/1KXxmcwd47x4v2SymyiBPK7ucn80PruSvcw4mZ5S3nWc/edit#slide=id.ge655fdfc4_0_7
Mongo-Hacker: https://github.com/TylerBrock/mongo-hacker - Funciona somente no linux

# Importar a base restaurante
c:\MongoAula>mongoimport --db be-mean --collection restaurantes --drop --file restaurantes.json

# Entrar na base
mongo be-mean

# Contar documentos da coleção
db.restaurantes.find({}).count()

MONGO
Instalação no windows: https://pablojuancruz.wordpress.com/2014/09/03/configurando-ambiente-mongodb-no-windows/

################################
# Aula 2 - MONGO
################################

Página: https://github.com/Webschool-io/be-mean-instagram/blob/master/apostila/classes/mongodb/class-02.md
Vídeo: https://www.youtube.com/watch?v=PaNVk0V2UNI&list=PL77JVjKTJT2jyVllJeO3TZV9D5cfSvSjR
Slide: https://docs.google.com/presentation/d/1KXxmcwd47x4v2SymyiBPK7ucn80PruSvcw4mZ5S3nWc/edit?pli=1

Inserir Registro
db.teste.insert({nome: "Suissa", idade: 30 })

Inserir Registro Com Variavel
var json = { escola: 'Webschool', active: true }
db.teste.insert(json)

Inserção de Pokemons:
var pokemon =  {'name':'Pikachu','description':'Rato elétrico bem fofinho','type': 'electric', attack: 55, height: 0.4 }
db.pokemons.insert(pokemon)
--
var pokemon = {'name':'Bulbassauro','description':'Chicote de trepadeira','type': 'grama', 'attack': 49, height: 0.4 }
db.pokemons.insert(pokemon)
---
var pokemon = {'name':'Charmander','description':'Esse é o cão chupando manga de fofinho','type': 'fogo', 'attack': 52, height: 0.6 }
db.pokemons.insert(pokemon)
---
var pokemon = {'name':'Squirtle','description':'Ejeta água que passarinho não bebe','type': 'água', 'attack': 48, height: 0.5 }
db.pokemons.insert(pokemon)

show dbs - Lista banco de dados
show collections - Lista as coleções/tabelas
query = { name: "Charizard"}
var p = db.pokemons.findOne(query)

Trabalhar com cursor:
var cur = db.pokemons.find();
while( cur.hasNext() ) { print(tojson(cur.next()))};




