# MongoDB - Aula 01 - Exercício
autor: Raphael Fuzaite

## Importando os restaurantes

    ```
    mongoimport --db be-mean --collection restaurantes --drop --file "C:\Development\be-mean-instagram\mongodb\data\restaurantes.json"
    2015-11-10T10:45:38.737-0200    connected to: localhost
	2015-11-10T10:45:38.740-0200    dropping: be-mean.restaurantes
	2015-11-10T10:45:40.320-0200    imported 25359 documents

    ```

## Contando os restaurantes

    ```
    raphael be-mean> db.restaurantes.find({}).count()
    25359

    ```