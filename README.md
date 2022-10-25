# Requêtes simples :
### Afficher le nom et la ville des clients

``` sql
SELECT nom, ville
FROM Clients;
```
### Afficher toutes les informations des clients

``` sql
SELECT *
FROM Clients;
```
## Elimination de doublons :
### Afficher la ville de tous les clients

``` sql
SELECT ALL ville
FROM Clients;
```
### Afficher toutes les villes sans doublons

``` sql
SELECT DISTINCT ville
FROM Clients;
```
##Selection (clause WHERE)

### Quels sont les clients dont la ville est ‘Aytré’ ?

``` sql
SELECT *
FROM Clients
WHERE ville = 'Aytré';
```
### Quels sont les films dont les prix de location sont supérieurs à 4.90 ?

``` sql
SELECT *
FROM Films
WHERE prix >= 4.90;
```
### Quels sont les locations réalisées après le 1er Novembre 2020 ?

``` sql
SELECT *
FROM Locations
WHERE date >= 2020-11-01
```
### Quels sont les clients dont le nom est soit Dupond, soit Dupont:

``` sql
SELECT *
FROM Clients
WHERE nom in ('Dupond', 'Dupont');
```

### Quels sont les films dont le titre commence par « Finding » ?

``` sql
SELECT *
FROM Films
WHERE titre LIKE 'Finding%';
```
### Quels sont les clients dont le nom commence par D et finit par d ?

``` sql
SELECT *
FROM Clients
WHERE nom LIKE 'D%d';
```

### Quels sont les clients qui n’ont pas de numéro de téléphone ?

``` sql
SELECT *
FROM Clients
WHERE telephone = '';
```

### Donner les films ordonnés selon l’ordre croissant de leurs titres?

``` sql
SELECT *
FROM Films
ORDER BY titre ASC;
```

### Donner les films ordonnés selon l’ordre décroissant de leurs prix?

``` sql
SELECT *
FROM Films
ORDER BY prix DESC;
```
### Donner le nombre de films en locations ?

``` sql
SELECT COUNT(*)
FROM Films;
```

### Donner tous les prix différents ?

``` sql
SELECT DISTINCT(prix)
FROM Films;
```
### Donner le nombre de films par prix ?

``` sql
SELECT prix,COUNT(*)
FROM Films
GROUP BY prix;
```
### Donner toutes les locations ?

``` sql
SELECT num_film, num_client
FROM Locations
```

##### Quels sont les films qui ont été loués?

``` sql
SELECT Locations.id_loc, Films.titre
FROM Films, Locations
WHERE Locations.num_film = Films.num;
```
##### ET par qui ?

``` sql
SELECT Locations.id_loc, Films.titre, Clients.nom
FROM Films, Locations, Clients
WHERE Locations.num_film = Films.num
AND Locations.num_client = Clients.num;
```
### Combien de films ont été loués par chaque personne ?

``` sql
SELECT Clients.nom, COUNT(*)
FROM Films, Locations, Clients
WHERE Locations.num_film = Films.num
AND Locations.num_client = Clients.num
GROUP BY Clients.nom;
```
### Combien de fois chaque film a été loue par client?

``` sql
SELECT Films.titre, COUNT(*)
FROM Films, Locations, Clients
WHERE Locations.num_film = Films.num
AND Locations.num_client = Clients.num
GROUP BY Films.titre;
```
### Et le plus loué ?

``` sql
SELECT Films.titre, COUNT(*)
FROM Films, Locations, Clients
WHERE Locations.num_film = Films.num
AND Locations.num_client = Clients.num
GROUP BY Films.titre
ORDER BY COUNT(*) DESC
LIMIT 1;
```
### Le cout moyen de location par client

``` sql
SELECT Clients.nom, AVG(Films.prix)
FROM Films, Locations, Clients
WHERE Locations.num_film = Films.num
AND Locations.num_client = Clients.num
GROUP BY Clients.nom;
```
