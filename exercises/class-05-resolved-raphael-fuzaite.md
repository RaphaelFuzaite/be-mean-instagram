# MongoDB - Aula 05 - Exercício
Autor: Raphael Fuzaite

## Importar as colections restaurantes e pokemons

    ```
	C:\Program Files\MongoDB\Server\3.0\bin>mongoimport --db be-mean-pokemons --collection pokemons --drop --file "C:\Development\Raphael\Dev\be-mean-instagram-mongodb\data\pokemons.json"
	2015-11-19T16:55:30.354-0200    connected to: localhost
	2015-11-19T16:55:30.356-0200    dropping: be-mean-pokemons.pokemons
	2015-11-19T16:55:30.471-0200    imported 610 documents
	
	C:\Program Files\MongoDB\Server\3.0\bin>
	```
	
## Distinct por `cuisine` na restaurantes

    ```
	> db.restaurantes.distinct('cuisine')
	[
			"Bakery",
			"Jewish/Kosher",
			"American ",
			"Delicatessen",
			"Ice Cream, Gelato, Yogurt, Ices",
			"Irish",
			"Other",
			"Chicken",
			"Hamburgers",
			"Turkish",
			"Caribbean",
			"Chinese",
			"Donuts",
			"Sandwiches/Salads/Mixed Buffet",
			"Bagels/Pretzels",
			"Pizza",
			"Continental",
			"Italian",
			"Steak",
			"Polish",
			"German",
			"Latin (Cuban, Dominican, Puerto Rican, South & Central American)",
			"French",
			"Pizza/Italian",
			"Mexican",
			"Spanish",
			"Café/Coffee/Tea",
			"Tex-Mex",
			"Pancakes/Waffles",
			"Soul Food",
			"Seafood",
			"Greek",
			"Hotdogs",
			"Not Listed/Not Applicable",
			"African",
			"Japanese",
			"Indian",
			"Armenian",
			"Thai",
			"Chinese/Cuban",
			"Mediterranean",
			"Korean",
			"Bottled beverages, including water, sodas, juices, etc.",
			"Russian",
			"Eastern European",
			"Middle Eastern",
			"Asian",
			"Ethiopian",
			"Vegetarian",
			"Barbecue",
			"Egyptian",
			"English",
			"Sandwiches",
			"Portuguese",
			"Indonesian",
			"Chinese/Japanese",
			"Filipino",
			"Juice, Smoothies, Fruit Salads",
			"Brazilian",
			"Afghan",
			"Vietnamese/Cambodian/Malaysia",
			"CafÃ©/Coffee/Tea",
			"Soups & Sandwiches",
			"Tapas",
			"Moroccan",
			"Pakistani",
			"Peruvian",
			"Bangladeshi",
			"Czech",
			"Salads",
			"Creole",
			"Fruits/Vegetables",
			"Iranian",
			"Cajun",
			"Scandinavian",
			"Polynesian",
			"Soups",
			"Australian",
			"Hotdogs/Pretzels",
			"Southwestern",
			"Nuts/Confectionary",
			"Hawaiian",
			"Creole/Cajun",
			"Californian",
			"Chilean"
	]
	>
	```	
	
## Distinct por `types` na pokemons

    ```
	> db.pokemons.distinct('types')
	[
			"normal",
			"fire",
			"bug",
			"flying",
			"poison",
			"electric",
			"steel",
			"water",
			"ice",
			"ghost",
			"fighting",
			"psychic",
			"grass",
			"ground",
			"fairy",
			"rock",
			"dark",
			"dragon"
	]
	>
	```
	
## As primeiras 3 páginas com .limit() e .skip() de pokemons (5 em 5)

    ```
	> db.pokemons.find({},{name:1}).limit(5).skip(3*0).pretty()
	{ "_id" : ObjectId("564b1dad25337263280d0479"), "name" : "Rattata" }
	{ "_id" : ObjectId("564b1dad25337263280d047b"), "name" : "Charmeleon" }
	{ "_id" : ObjectId("564b1dad25337263280d047e"), "name" : "Caterpie" }
	{ "_id" : ObjectId("564b1dad25337263280d047f"), "name" : "Metapod" }
	{ "_id" : ObjectId("564b1dad25337263280d0480"), "name" : "Butterfree" }
	> db.pokemons.find({},{name:1}).limit(5).skip(3*1).pretty()
	{ "_id" : ObjectId("564b1dad25337263280d047f"), "name" : "Metapod" }
	{ "_id" : ObjectId("564b1dad25337263280d0480"), "name" : "Butterfree" }
	{ "_id" : ObjectId("564b1dad25337263280d0481"), "name" : "Spearow" }
	{ "_id" : ObjectId("564b1dad25337263280d0482"), "name" : "Kakuna" }
	{ "_id" : ObjectId("564b1dae25337263280d0483"), "name" : "Farfetchd" }
	> db.pokemons.find({},{name:1}).limit(5).skip(3*2).pretty()
	{ "_id" : ObjectId("564b1dad25337263280d0482"), "name" : "Kakuna" }
	{ "_id" : ObjectId("564b1dae25337263280d0483"), "name" : "Farfetchd" }
	{ "_id" : ObjectId("564b1dae25337263280d0484"), "name" : "Magnemite" }
	{ "_id" : ObjectId("564b1dae25337263280d0486"), "name" : "Doduo" }
	{ "_id" : ObjectId("564b1dae25337263280d0487"), "name" : "Seel" }
	>
	```	
	
## Group ou Aggregate contando a quantidade de pokemons de cada tipo

    ```		
	> db.pokemons.aggregate([{$match:{types:'fire'}},{$group: {_id:{}, total: {$sum: 1}}}]).pretty()
	{ "_id" : { }, "total" : 47 }
	>
	```
	
## Realizar 3 counts em pokemons: (todos, tipo fogo e quantos tem defesa maoir que 70)

    ```
	> db.pokemons.count()
	610
	> db.pokemons.count({types: 'fire'})
	47
	> db.pokemons.count({defense: {$gt: 70}})
	250
	>
	```