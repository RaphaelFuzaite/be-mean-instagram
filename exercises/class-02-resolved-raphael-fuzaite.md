# MongoDB - Aula 02 - Exercício
Autor: Raphael Fuzaite

## Criando database be-mean-pokemons

    ```

    PC@RAPHAEL /C/Program Files/MongoDB/Server/3.0/bin
    $ mongo
    MongoDB shell version: 3.0.3
    connecting to: test
    > use be-mean-pokemons
    switched to db be-mean-pokemons
    >

    ```

## Listando databases do servidor

    ```

    > show dbs
    be-mean       0.078GB
    local         0.078GB
    >

    ```
    
## Listando collections

    ```

    > show collections

    ```   
    
## Inserindo pokemons

    ```

    > var pokemons = [{
    ...             "name":"Raikou",
    ...             "description":"Raikou embodies the speed of lightning.",
    ...             "type": "Eletric",
    ...             "attack": 85,
    ...             "height": 1.9,
    ...             "defense": 75
    ...         },
    ...         {
    ...             "name":"Entei",
    ...             "description":"Entei embodies the passion of magma.",
    ...             "type": "Fire",
    ...             "attack": 115,
    ...             "height": 2.1,
    ...             "defense": 85
    ...         },
    ...         {
    ...             "name":"Suicune",
    ...             "description":"Suicune embodies the compassion of a pure spring of water.",
    ...             "type": "Water",
    ...             "attack": 75,
    ...             "height": 2.0,
    ...             "defense": 115
    ...         },
    ...         {
    ...             "name":"Venusaur",
    ...             "description":"There is a large flower on Venusaur's back.",
    ...             "type": "Grass",
    ...             "attack": 82,
    ...             "height": 2.0,
    ...             "defense": 83
    ...         },
    ...         {
    ...             "name":"Charizard",
    ...             "description":"Charizard flies around the sky in search of powerful opponents.",
    ...             "type": "Fire",
    ...             "attack": 84,
    ...             "height": 1.7,
    ...             "defense": 78
    ...         },
    ...         {
    ...             "name":"Blastoise",
    ...             "description":"Blastoise has water spouts that protrude from its shell.",
    ...             "type": "Water",
    ...             "attack": 83,
    ...             "height": 1.6,
    ...             "defense": 100
    ...         }]
    > db.pokemons.save(pokemons)
    BulkWriteResult({
            "writeErrors" : [ ],
            "writeConcernErrors" : [ ],
            "nInserted" : 6,
            "nUpserted" : 0,
            "nMatched" : 0,
            "nModified" : 0,
            "nRemoved" : 0,
            "upserted" : [ ]
    })
    >

    ```      
    
## Listando pokemons da coleção

    ```
    
    > db.pokemons.find()
    { 
        "_id" : ObjectId("5643550bb1dbcf28b86b63de"), 
        "name" : "Raikou", 
        "description" : "Raikou embodies the speed of lightning.", 
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
        "attack" : 75, 
        "height" : 2, 
        "defense" : 115 
    }
    { 
        "_id" : ObjectId("5643550bb1dbcf28b86b63e1"), 
        "name" : "Venusaur", 
        "description" : "There is a large flower on Venusaur's back.", 
        "type" : "Grass", 
        "attack" : 82, 
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
    
## Modificando descrição

    ```    
    > var poke = db.pokemons.findOne({"name": "Raikou"})
    > poke
    {
        "_id" : ObjectId("5643550bb1dbcf28b86b63de"),
        "name" : "Raikou",
        "description" : "Raikou embodies the speed of lightning.",
        "type" : "Eletric",
        "attack" : 85,
        "height" : 1.9,
        "defense" : 75
    }
    > poke.description = "Raikou's roar send shock waves shuddering through the air"
    Raikou's roar send shock waves shuddering through the air
    > db.pokemons.save(poke)
    WriteResult({
            "nMatched" : 1,
            "nUpserted" : 0,
            "nModified" : 1
    })
    > db.pokemons.findOne({"name": "Raikou"})
    {
        "_id" : ObjectId("5643550bb1dbcf28b86b63de"),
        "name" : "Raikou",
        "description" : "Raikou embodies the speed of lightning.",
        "type" : "Eletric",
        "attack" : 85,
        "height" : 1.9,
        "defense" : 75
    }
    >

    ```