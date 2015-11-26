# MongoDB - Aula 04 - Exercício
autor: Fabiano Cacin Pinel

## Dicionário:
$set - O operador $set modifica um valor ou cria ele, caso não exista.
{ $set : { campo : valor } }

$inc - O operador $inc incrementa um valor no campo com a quantidade desejada.

$unset - para remover os campos, que é o caso do $unset.

$push - $push adiciona um valor ao um campo de array.

$pushAll - Adiciona vários campos atraves de um array

$pull - remove o valor do campo, caso o campo seja um *Array* existente. Caso não exista ele não fará nada.

$pullAll - Remove varios valores de um array
options - Servirá para configurarmos alguns valores diferentes do padrão para o update.
{
  upsert: boolean, O parâmetro upsert serve para caso o documento não seja encontrado pela query ele insira o objeto que está sendo passado como modificação.
  multi: boolean, Permite o update atualizar todos os registros
  writeConcern: O writeConcern descreve a garantia de que MongoDB fornece ao relatar o sucesso de uma operação de escrita.
}

$setOnInsert - Se não achar o valor, ele cadastra com os parametros que foi passado

$in - O operador $in retorna o(s) documento(s) que possui(em) algum dos valores passados no [Array_de_valores].

$nin - Retorna documentos se nenhum dos valores do array for encontrado.

$all - Retorna documentos se todos os valores do array foram encontrados.

$ne - Não igual

writeConcern - 

##  1 - Adicionar 2 ataques ao mesmo tempo para os seguintes pokemons: Ivysaur, Venusaur, Charmander e Charmeleon.
```
var query = { name: /Ivysaur/i }
var mod = { $pushAll: { moves: ['espada juticeira', 'investida trovão'] }}
db.pokemons.update(query, mod)

var query = { name: /Venusaur/i }
var mod = { $pushAll: { moves: ['radiação', 'giro rápido']} }
db.pokemons.update(query, mod)

var query = { name: /Charmander/i }
var mod = { $pushAll: { moves: ['pistola', 'dança de pétalas'] } }
db.pokemons.update(query, mod)

var query = { name: /Charmeleon/i }
var mod = { $pushAll: { moves: ['pedaço de pau', 'pedra'] } }
db.pokemons.update(query, mod)
```
## 2 - Adicionar 1 movimento em todos os pokemons: desvio.
```
var query 	= { }
var mod 	= { $push: { moves: 'desvio' } }
var options = { multi: true }
db.pokemons.update(query, mod, options)
```
## 3 - Adicionar o pokemon AindaNaoExisteMon caso ele não exista com todos os dados com o valor null e a descrição: "Sem maiores informações".
```
var query = {name: /AindaNaoExisteMon/i}
var mod = {$setOnInsert:
    {
      name: 		'AindaNaoExisteMon',
      type: 		null,
      attack: 		null,
      defense: 		null,
      height: 		null,
      description: 'Sem maiores informações'
    }
}

var options = { upsert: true }
db.pokemons.update(query, mod, options)
```
4 - Pesquisar todos o pokemons que possuam o ataque investida e mais um que você adicionou.
```
var query = {attack: {$in: [/pedra/i]}}
db.pokemons.find(query)
```
5 - Pesquisar todos os pokemons que possuam os ataques que você adicionou.
```
var query = {attack: {$all: [/investida/i, /pedra/i]}}
db.pokemons.find(query)
{
    "_id" : ObjectId("56563e5d2c37368ad25f89a2"),
    "name" : "Charmeleon",
    "description" : "Tartaruga pokemon do mal",
    "defense" : 60.0000000000000000,
    "height" : 1.1000000000000001,
    "moves" : [ 
        "pedaço de pau", 
        "pedra", 
        "desvio"
    ],
    "attack" : [ 
        "investida", 
        "pedra"
    ]
}
```
## 6 - Pesquisar todos os pokemons que não são do tipo elétrico.
```
var query = {type: {$not: /elétrico/i}}
db.pokemons.find(query)

{
    "_id" : ObjectId("565513af40ffb2868cb8e054"),
    "name" : "Bulbasaur",
    "description" : "Bichinho verdinho e feinho",
    "defense" : 55.0000000000000000,
    "height" : 0.7000000000000000,
    "moves" : [ 
        "desvio"
    ]
}

{
    "_id" : ObjectId("56563e5d2c37368ad25f899f"),
    "name" : "Ivysaur",
    "description" : "Mesmo bichinho verdinho e feinho mas tem asas",
    "defense" : 56.0000000000000000,
    "height" : 4.0000000000000000,
    "moves" : [ 
        "espada juticeira", 
        "investida trovão", 
        "desvio"
    ]
}

{
    "_id" : ObjectId("56563e5d2c37368ad25f89a0"),
    "name" : "Venusaur",
    "description" : "Bichinho feinho com um abacaxi na cabeça",
    "defense" : 58.0000000000000000,
    "height" : 2.0000000000000000,
    "moves" : [ 
        "radiação", 
        "giro rápido", 
        "desvio"
    ]
}

{
    "_id" : ObjectId("56563e5d2c37368ad25f89a1"),
    "name" : "Charmander",
    "description" : "Tartaruga pokemon",
    "defense" : 10.0000000000000000,
    "height" : 0.6000000000000000,
    "moves" : [ 
        "pistola", 
        "dança de pétalas", 
        "desvio"
    ]
}

{
    "_id" : ObjectId("56563e5d2c37368ad25f89a2"),
    "name" : "Charmeleon",
    "description" : "Tartaruga pokemon do mal",
    "defense" : 60.0000000000000000,
    "height" : 1.1000000000000001,
    "moves" : [ 
        "pedaço de pau", 
        "pedra", 
        "desvio"
    ],
    "attack" : [ 
        "investida", 
        "pedra"
    ]
}

{
    "_id" : ObjectId("56563e5e2c37368ad25f89a3"),
    "name" : "Charizard",
    "description" : "Drãgão galã",
    "defense" : 16.0000000000000000,
    "height" : 1.7000000000000000,
    "moves" : [ 
        "desvio"
    ]
}

{
    "_id" : ObjectId("565648d02d24173927206925"),
    "name" : "AindaNaoExisteMon",
    "type" : null,
    "defense" : null,
    "height" : null,
    "description" : "Sem maiores informações"
}
```
## 7 - Pesquisar todos os pokemons que tenham o ataque investida E tenham a defesa não menor ou igual a 49.
```
var query = {$and: [ {moves: {$in: ['investida']}}, {attack: {$not: {$lte: 49}}} ]}
db.pokemons.find(query)

Fetched 0 record(s) in 172ms

```
## 8 - Remova todos os pokemons do tipo água e com attack menor que 50.
```
var query = {$and: [ {type: /água/i}, {attack: {$lt: 50}} ]}
db.pokemons.remove(query)

Removed 0 record(s) in 151ms
```

## 9 - Esse item não está no vídeo e se você fizer significa que você lê as coisas, nesse exercício demonstre qual a diferença entre os operadores $ne e $not.
```
$ne - seleciona os documentos onde o valor do campo não é igual (ou seja, !=) o valor especificado. Isto inclui documentos que não contêm o campo.

$not - O $not nega um operador, por exemplo a query db.inventory.find( { price: { $not: { $gt: 1.99 } } } ) retornará todos documentos que NÂO sejam maiores que 1.99.
```