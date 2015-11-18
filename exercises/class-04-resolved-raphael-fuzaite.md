# MongoDB - Aula 04 - Exercício
Autor: Raphael Fuzaite

## Adicionar 2 ataques ao mesmo tempo para os pokemons: Entei, Raikou e Suicune

    ```
	> var query = { $or: [ { name: /entei/i }, { name: /raikou/i }, { name: /suicune/i } ] };
    > var mod = { $pushAll: { moves: ['Manobra evasiva', 'Investida'] } };
    > var opt = { multi: true };
    > db.pokemons.update(query, mod, opt);
    WriteResult({
        "nMatched" : 3, 
        "nUpserted" : 0, 
        "nModified" : 3
    })
    
    ```	
    
## Adicionar 1 movimento em todos os pokemons: Manobra evasiva

    ```
	
    > var query = { moves: { $nin: ['Manobra evasiva'] } };
    > var mod = { $push: { moves: ['Manobra evasiva'] } };
    > var opt = { multi: true };
    > db.pokemons.update(query, mod, opt);
    WriteResult({ 
        "nMatched" : 3, 
        "nUpserted" : 0, 
        "nModified" : 3 
    })
    
    ```
    
## Adicionar o pokemon AindaNaoExisteMon caso ele não exista com todos os dados com o valor null e a descrição: "Sem maiores informações".

    ```
	> var query = { name: /AindaNaoExisteMon/i };
    > var mod = { $setOnInsert: {
    ...         name: "AindaNaoExisteMon",
    ...         type: null,
    ...         moves: [],
    ...         attack: null,
    ...         height: null,
    ...         defense: null,
    ...         description: "Sem maiores informações"
    ...       } }
    > var opt = { upsert: true };
    > db.pokemons.update(query, mod, opt);
    WriteResult({
            "nMatched" : 0,
            "nUpserted" : 1,
            "nModified" : 0,
            "_id" : ObjectId("564ca184fe10a3380522a23d")
    })     
     
    
    ```
    
## Pesquisar todos o pokemons que possuam o ataque Investida e mais um que você adicionou.

    ```
	> var query = { $or: [ { name: /entei/i }, { name: /raikou/i }, { name: /suicune/i } ] };
    > var mod = { $push: { moves: [ 'Rugido' ] } };
    > var opt = { multi: true };
    > db.pokemons.update(query, mod, opt);
    WriteResult({ 
        "nMatched" : 3, 
        "nUpserted" : 0, 
        "nModified" : 3 
    })
    > var query = { moves: { $in: [/investida/i, /rugido/i] } };
    > db.pokemons.find(query);
    { "_id" : ObjectId("564c7b11492be4593a6b4749"), "name" : "Entei", "description"
    : "Entei embodies the passion of magma.", "type" : "Fire", "attack" : 115, "heig
    ht" : 2.1, "defense" : 85, "moves" : [ "Manobra evasiva", "Investida", [ "Rugido
    " ] ] }
    { "_id" : ObjectId("564c7b11492be4593a6b4748"), "name" : "Raikou", "description"
    : "Raikou's roar send shock waves shuddering through the air", "type" : "Eletri
    c", "attack" : 85, "height" : 1.9, "defense" : 75, "moves" : [ "Manobra evasiva"
    , "Investida", [ "Rugido" ] ] }
    { "_id" : ObjectId("564c7b11492be4593a6b474a"), "name" : "Suicune", "description
    " : "Suicune embodies the compassion of a pure spring of water.", "type" : "Wate
    r", "attack" : 75, "height" : 2, "defense" : 115, "moves" : [ "Manobra evasiva",
    "Investida", [ "Rugido" ] ] }
    >
    
    ```
    
## Pesquisar todos os pokemons que possuam os ataques que você adicionou, escolha seu pokemon favorito.

    ```
    > var query = { moves: { $in: /rugido/i] } };
    > db.pokemons.find(query);
    { "_id" : ObjectId("564c7b11492be4593a6b4749"), "name" : "Entei", "description"
    : "Entei embodies the passion of magma.", "type" : "Fire", "attack" : 115, "heig
    ht" : 2.1, "defense" : 85, "moves" : [ "Manobra evasiva", "Investida", [ "Rugido
    " ] ] }
    { "_id" : ObjectId("564c7b11492be4593a6b4748"), "name" : "Raikou", "description"
    : "Raikou's roar send shock waves shuddering through the air", "type" : "Eletri
    c", "attack" : 85, "height" : 1.9, "defense" : 75, "moves" : [ "Manobra evasiva"
    , "Investida", [ "Rugido" ] ] }
    { "_id" : ObjectId("564c7b11492be4593a6b474a"), "name" : "Suicune", "description
    " : "Suicune embodies the compassion of a pure spring of water.", "type" : "Wate
    r", "attack" : 75, "height" : 2, "defense" : 115, "moves" : [ "Manobra evasiva",
    "Investida", [ "Rugido" ] ] }
    >
    
    ```
    
## Pesquisar todos os pokemons que não são do tipo elétrico.

    ```
    > var query = { type: { $ne: 'Eletric' } };
    > db.pokemons.find(query)
    { "_id" : ObjectId("564c7b11492be4593a6b4749"), "name" : "Entei", "description"
    : "Entei embodies the passion of magma.", "type" : "Fire", "attack" : 115, "heig
    ht" : 2.1, "defense" : 85, "moves" : [ "Manobra evasiva", "Investida", [ "Rugido
    " ] ] }
    { "_id" : ObjectId("564c7b11492be4593a6b474b"), "name" : "Venusaur", "descriptio
    n" : "There is a large flower on Venusaur's back.", "type" : "Grass", "attack" :
    82, "height" : 2, "defense" : 83, "moves" : [ [ "Manobra evasiva" ] ] }
    { "_id" : ObjectId("564c7b11492be4593a6b474c"), "name" : "Charizard", "descripti
    on" : "Charizard flies around the sky in search of powerful opponents.", "type"
    : "Fire", "attack" : 84, "height" : 1.7, "defense" : 78, "moves" : [ [ "Manobra
    evasiva" ] ] }
    { "_id" : ObjectId("564c7b11492be4593a6b474d"), "name" : "Blastoise", "descripti
    on" : "Blastoise has water spouts that protrude from its shell.", "type" : "Wate
    r", "attack" : 83, "height" : 1.6, "defense" : 100, "moves" : [ [ "Manobra evasi
    va" ] ] }
    { "_id" : ObjectId("564ca184fe10a3380522a23d"), "name" : "AindaNaoExisteMon", "t
    ype" : null, "moves" : [ ], "attack" : null, "height" : null, "defense" : null,
    "description" : "Sem maiores informações" }
    { "_id" : ObjectId("564c7b11492be4593a6b474a"), "name" : "Suicune", "description
    " : "Suicune embodies the compassion of a pure spring of water.", "type" : "Wate
    r", "attack" : 75, "height" : 2, "defense" : 115, "moves" : [ "Manobra evasiva",
    "Investida", [ "Rugido" ] ] }
    >	
    
    ```
    
## Pesquisar todos pokemons que tenham o ataque Investida e tenham a defesa não menor ou igual a 49.

    ```
	> var query = { $and: [{ moves: { $in: [/investida/i] } }, { defense: { $gt: 80 }  }] };
    > db.pokemons.find(query)
    { "_id" : ObjectId("564c7b11492be4593a6b4749"), "name" : "Entei", "description"
    : "Entei embodies the passion of magma.", "type" : "Fire", "attack" : 115, "heig
    ht" : 2.1, "defense" : 85, "moves" : [ "Manobra evasiva", "Investida", [ "Rugido
    " ] ] }
    { "_id" : ObjectId("564c7b11492be4593a6b474a"), "name" : "Suicune", "description
    " : "Suicune embodies the compassion of a pure spring of water.", "type" : "Wate
    r", "attack" : 75, "height" : 2, "defense" : 115, "moves" : [ "Manobra evasiva",
    "Investida", [ "Rugido" ] ] }
    
    ```
    
## Remova todos os pokemons do tipo água e com attack menor que 50.

    ```
    
	> var query = { $and: [ { type: /water/i }, { attack: { $lt: 80 } }] };
    > db.pokemons.remove(query);
    > Removed 1 record(s) in 10ms
    WriteResult({
        "nRemoved": 1
    })
    
    ```    