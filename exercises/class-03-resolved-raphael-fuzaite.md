# MongoDB - Aula 03 - Exercício
Autor: Raphael Fuzaite

## Listando pokemons com altura menor que 0.5

    ```

    PC@RAPHAEL /C/Program Files/MongoDB/Server/3.0/bin
    $ mongo
    MongoDB shell version: 3.0.3
    connecting to: test
    > use be-mean-pokemons
    switched to db be-mean-pokemons
    >
    > var query = {"height": {$lt: 0.5}}
    > db.pokemons.find(query)

    ```

## Listando pokemons com a altura maior ou igual a 0.5

    ```

    > var query = {"height": {$gte: 0.5}}
    > db.pokemons.find(query)
    {
        "_id" : ObjectId("5643550bb1dbcf28b86b63de"), 
        "name" : "Raikou",
        "description": "Raikou's roar send shock waves shuddering through the air",
        "type" : "Eletric", 
        "attack" : 85, 
        "height" : 1.9, 
        "defense" : 75 
    }
    { 
        "_id" : ObjectId("5643550bb1dbcf28b86b63df"), 
        "name" : "Entei",
        "description": "Entei embodies the passion of magma.", 
        "type" : "Fire", 
        "attack" : 115, 
        "height" : 2.1, 
        "defense" : 85 
    }
    {
        "_id" : ObjectId("5643550bb1dbcf28b86b63e0"), 
        "name" : "Suicune",
        "description" : "Suicune embodies the compassion of a pure spring of water.", 
        "type" : "Water", 
        attack" : 75, 
        "height" : 2, 
        "defense" : 115 
    }
    { 
        "_id" : ObjectId("5643550bb1dbcf28b86b63e1"),
        "name" : "Venusaur",
        "description" : "There is a large flower on Venusaur's back.", 
        "type" : "Grass",
        "attack" :82,
        "height" : 2,
        "defense" : 83 
    }
    {
        "_id" : ObjectId("5643550bb1dbcf28b86b63e2"), 
        "name" : "Charizard",
        "description" : "Charizard flies around the sky in search of powerful opponents.", 
        "type": "Fire", 
        "attack" : 84, 
        "height" : 1.7, 
        "defense" : 78 
    }
    {
        "_id" : ObjectId("5643550bb1dbcf28b86b63e3"), 
        "name" : "Blastoise",
        "description" : "Blastoise has water spouts that protrude from its shell.", 
        "type" : "Water", 
        "attack" : 83, 
        "height" : 1.6, 
        "defense" : 100
    }

    ```
    
## Listando pokemons com altura maior ou igual a 0.5 e do tipo grama

    ```

    > var query = {$and: [{"height": {$gte: 0.5}},{"type": "Grass"}]}
    > db.pokemons.find(query)
    {
        "_id" : ObjectId("5643550bb1dbcf28b86b63e1"),
        "name" : "Venusaur",
        "description" : "There is a large flower on Venusaur's back.",
        "type" : "Grass", 
        "attack" :82, 
        "height" : 2, 
        "defense" : 83 
    }
    >

    ```   
    
## Listando pokemons com o nome 'Pikachu' ou ataque menor ou igual a 0.5

    ```

    > var query = {$or: [{"attack": {$lte: 0.5}},{"name": "Pikachu"}]}
    > db.pokemons.find(query)
    >

    ```      
    
## Listando pokemons com ataque maior ou igual a 84 e com altura maior ou igual a 0.5

    ```
    
    > var query = {$and: [{"attack": {$gte: 84}},{"height": {$gte: 0.5}}]}
    > db.pokemons.find(query)
    {
        "_id" : ObjectId("5643550bb1dbcf28b86b63de"), 
        "name" : "Raikou", 
        "description": "Raikou's roar send shock waves shuddering through the air", 
        "type" : "Eletric", 
        "attack" : 85, 
        "height" : 1.9, 
        "defense" : 75 
    }
    {
        "_id" : ObjectId("5643550bb1dbcf28b86b63df"), 
        "name" : "Entei", 
        "description": "Entei embodies the passion of magma.", 
        "type" : "Fire", 
        "attack" : 115, 
        "height" : 2.1, 
        "defense" : 85 
    }
    { 
        "_id" : ObjectId("5643550bb1dbcf28b86b63e2"), 
        "name" : "Charizard", 
        "description" : "Charizard flies around the sky in search of powerful opponents.", 
        "type": "Fire", 
        "attack" : 84, 
        "height" : 1.7, 
        "defense" : 78 
    }
    >

    ```