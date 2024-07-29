# Exercices SQL

Ce dépôt contient des exercices SQL pour différentes requêtes. Voici la liste des exercices :

## Requete 1. Nom et année de naissance des artistes nés avant 1950.
localhost:3306/films/artiste/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=film

   Affichage des lignes 0 - 24 (total de 540, traitement en 0,0012 seconde(s).)


SELECT nom, prénom, annéeNaiss
FROM artiste
WHERE annéeNaiss < 1950;


nom	prénom	annéeNaiss	
Lucas	George	1944	
Ford	Harrison	1942	
Cushing	Peter	1913	
Daniels	Anthony	1946	
Brooks	Albert	1947	
Welles	Orson	1915	
Deneuve	Catherine	1943	
Holm	Ian	1931	
Lang	Fritz	1890	
Lee	Christopher	1922	
Baker	Kenny	1934	
Carradine	David	1936	
Eastwood	Clint	1930	
Freeman	Morgan	1937	
Hackman	Gene	1930	
Harris	Richard	1930	
Wilkinson	Tom	1948	
Cronenberg	David	1943	
Kubrick	Stanley	1928	
Dullea	Keir	1936	
Lockwood	Gary	1937	
Sylvester	William	1922	
Rain	Douglas	1928	
Plummer	Christopher	1929	
Glenn	Scott	1941	


## Requete 2. Titre de tous les drames.
localhost:3306/films/film/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=artiste

   Affichage des lignes 0 - 24 (total de 83, traitement en 0,0004 seconde(s).)


SELECT titre
FROM film
WHERE genre = 'Drame';


titre	
Apocalypse Now	
A History of Violence	
Match point	
Le Secret de Brokeback Mountain	
Breaking the Waves	
Les Quatre Cents Coups	
Lost in Translation	
The Dark Knight : Le Chevalier noir	
Le Nom de la rose	
Rebecca	
Le Parrain	
Le Parrain, 2ème partie	
Le Mépris	
À bout de souffle	
Casablanca	
Le Bateau	
Le Pianiste	
La liste de Schindler	
Vol au dessus d'un nid de coucou	
Fight Club	
Fenêtre sur cour	
Solaris	
Titanic	
Boulevard du Crépuscule	
Usual Suspects	

  
## Requete 3. Quels rôles a joué Bruce Willis.
localhost:3306/films/role/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=film

   Affichage des lignes 0 -  4 (total de 5, traitement en 0,0011 seconde(s).)


SELECT role.nomRôle
FROM artiste
JOIN role ON artiste.idArtiste = role.idActeur
WHERE artiste.nom = 'Willis' AND artiste.prénom = 'Bruce';


nomRôle	
John McClane	
Butch Coolidge	
John McClane	
John McClane	
John McClane	


## Requete 4. Qui est le réalisateur de Memento.
localhost:3306/films/artiste/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=role

   Affichage des lignes 0 -  0 (total de 1, traitement en 0,0010 seconde(s).)


SELECT artiste.nom, artiste.prénom
FROM film
JOIN artiste ON film.idRéalisateur = artiste.idArtiste
WHERE film.titre = 'Memento';



Nolan	Christopher	



## Requete 5. Quelles sont les notes obtenues par le film Fargo.
localhost:3306/films/notation/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=artiste

   Affichage des lignes 0 -  0 (total de 1, traitement en 0,0020 seconde(s).)


SELECT note
FROM notation
JOIN film ON notation.idFilm = film.idFilm
WHERE film.titre = 'Fargo';



6	



## Requete 6. Qui a joué le rôle de Chewbacca ?
localhost:3306/films/artiste/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=notation

   Affichage des lignes 0 -  4 (total de 5, traitement en 0,0014 seconde(s).)


SELECT artiste.nom, artiste.prénom
FROM artiste
JOIN role ON artiste.idArtiste = role.idActeur
WHERE role.nomRôle = 'Chewbacca';


nom	prénom	
Mayhew	Peter	
Mayhew	Peter	
Mayhew	Peter	
Mayhew	Peter	
Suotamo	Joonas	



## Requete 7. Dans quels films Bruce Willis a-t-il joué le rôle de John McClane ?
  SELECT film.titre FROM film JOIN role ON film.idFilm = role.idFilm JOIN artiste ON role.idActeur = artiste.idArtiste WHERE artiste.nom = 'Willis' AND artiste.prénom = 'Bruce' AND role.nomRôle = 'John McClane';
titre
Piège de cristal
Die Hard 4 : Retour en enfer
Une Journée en enfer
58 minutes pour vivre

## Requete 8. Nom des acteurs de 'Sueurs froides'.
  SELECT artiste.nom, artiste.prénom FROM artiste JOIN role ON artiste.idArtiste = role.idActeur JOIN film ON role.idFilm = film.idFilm WHERE film.titre = 'Sueurs froides';
tewart Jam
Novak Kim
Bel Geddes Bar 


## Requete 9. Quelles sont les films notés par l'internaute Prénom 0 Nom0.
  SELECT film.titre FROM film JOIN notation ON film.idFilm = notation.idFilm JOIN internaute ON notation.email = internaute.email WHERE internaute.prénom = 'Prénom0' AND internaute.nom = 'Nom0';
Eternal Sunshine of the Spotless Mind
Les Aventuriers de l'arche perdue
Le Secret de Brokeback Mountain
The Dark Knight : Le Chevalier noir
Minority Report
Terminator
Le Parrain, 3ème partie
Batman Begins
Jurassic Park
Eyes Wide Shut
Kill Bill : Volume 2
Reservoir Dogs
Fight Club
Piège de cristal
Matrix Reloaded
Pulp Fiction
Shining
Volte/Face
Seven
Rencontres du troisième type
L'Empire contre-attaque
Star Wars, épisode I - La Menace fantôme
RoboCop
No Country For Old Men
Inception

## Requete 10. Films dont le réalisateur est Tim Burton, et l’un des acteurs Johnny Depp.
  localhost:3306/films/film/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=film

   Affichage des lignes 0 -  0 (total de 1, traitement en 0,0021 seconde(s).)


SELECT film.titre
FROM film
JOIN artiste AS réalisateur ON film.idRéalisateur = réalisateur.idArtiste
JOIN role ON film.idFilm = role.idFilm
JOIN artiste AS acteur ON role.idActeur = acteur.idArtiste
WHERE réalisateur.nom = 'Burton' AND réalisateur.prénom = 'Tim'
AND acteur.nom = 'Depp' AND acteur.prénom = 'Johnny';



Sleepy Hollow, La Légende du cavalier sans tête	


## Requete 11. Titre des films dans lesquels a joué Woody Allen. Donner aussi le rôle.
localhost:3306/films/film/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=film

   Affichage des lignes 0 -  3 (total de 4, traitement en 0,0011 seconde(s).)


SELECT film.titre, role.nomRôle
FROM film
JOIN role ON film.idFilm = role.idFilm
JOIN artiste ON role.idActeur = artiste.idArtiste
WHERE artiste.nom = 'Allen' AND artiste.prénom = 'Woody';


titre	nomRôle	
Scoop	Sid Waterman	
Manhattan	Isaac Davis	
Annie Hall	Alvy Singer	
Maris et femmes	Prof. Gabriel 'Gabe' Roth	


## Requete 12. Quel metteur en scène a tourné dans ses propres films ? Donner le nom, le rôle et le titre des films.
localhost:3306/films/film/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=film

   Affichage des lignes 0 - 16 (total de 17, traitement en 0,0030 seconde(s).)


SELECT réalisateur.nom, réalisateur.prénom, role.nomRôle, film.titre
FROM artiste AS réalisateur
JOIN film ON réalisateur.idArtiste = film.idRéalisateur
JOIN role ON film.idFilm = role.idFilm
WHERE réalisateur.idArtiste = role.idActeur;


nom	prénom	nomRôle	titre	
Eastwood	Clint	Bill Munny	Impitoyable	
Tarantino	Quentin	Mr. Brown	Reservoir Dogs	
Allen	Woody	Sid Waterman	Scoop	
Tarantino	Quentin	Jimmie Dimmick	Pulp Fiction	
Allen	Woody	Isaac Davis	Manhattan	
Allen	Woody	Alvy Singer	Annie Hall	
Kelly	Gene	Don Lockwood	Chantons sous la pluie	
Chaplin	Charlie	Adenoid Hynkel, Dictator of Tomania / A Jewish Bar...	Le dictateur	
Polanski	Roman	Alfred, Assistent des Professors	Le Bal des vampires	
Chaplin	Charlie	A factory worker	Les temps modernes	
Welles	Orson	Michael O'Hara	La Dame de Shanghai	
Lee Jones	Tommy	Pete Perkins	Trois enterrements	
Chaplin	Charlie	A Tramp	Le Kid	
Allen	Woody	Prof. Gabriel 'Gabe' Roth	Maris et femmes	
Chaplin	Charlie	Calvero	Les feux de la rampe	
Cassavetes	John	Maurice Aarons	Opening Night	
Podalydès	Bruno	Michel	Comme un avion	


## Requete 13. Titre des films de Quentin Tarantino dans lesquels il n’a pas joué.
localhost:3306/films/film/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=film

   Affichage des lignes 0 -  4 (total de 5, traitement en 0,0041 seconde(s).)


SELECT film.titre
FROM film
JOIN artiste ON film.idRéalisateur = artiste.idArtiste
WHERE artiste.nom = 'Tarantino' AND artiste.prénom = 'Quentin'
AND film.idFilm NOT IN (
    SELECT role.idFilm
    FROM role
    JOIN artiste ON role.idActeur = artiste.idArtiste
    WHERE artiste.nom = 'Tarantino' AND artiste.prénom = 'Quentin'
);


titre	
Kill Bill : Volume 1	
Jackie Brown	
Kill Bill : Volume 2	
Inglourious Basterds	
Django Unchained	


## Requete 14. Quel metteur en scène a tourné en tant qu’acteur ? Donner le nom, le rôle et le titre des films dans lesquels cet artiste a joué.
localhost:3306/films/film/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=film

   Affichage des lignes 0 - 16 (total de 17, traitement en 0,0020 seconde(s).)


SELECT DISTINCT réalisateur.nom, réalisateur.prénom, role.nomRôle, film.titre
FROM artiste AS réalisateur
JOIN film ON réalisateur.idArtiste = film.idRéalisateur
JOIN role ON film.idFilm = role.idFilm
WHERE réalisateur.idArtiste = role.idActeur;


nom	prénom	nomRôle	titre	
Eastwood	Clint	Bill Munny	Impitoyable	
Tarantino	Quentin	Mr. Brown	Reservoir Dogs	
Allen	Woody	Sid Waterman	Scoop	
Tarantino	Quentin	Jimmie Dimmick	Pulp Fiction	
Allen	Woody	Isaac Davis	Manhattan	
Allen	Woody	Alvy Singer	Annie Hall	
Kelly	Gene	Don Lockwood	Chantons sous la pluie	
Chaplin	Charlie	Adenoid Hynkel, Dictator of Tomania / A Jewish Bar...	Le dictateur	
Polanski	Roman	Alfred, Assistent des Professors	Le Bal des vampires	
Chaplin	Charlie	A factory worker	Les temps modernes	
Welles	Orson	Michael O'Hara	La Dame de Shanghai	
Lee Jones	Tommy	Pete Perkins	Trois enterrements	
Chaplin	Charlie	A Tramp	Le Kid	
Allen	Woody	Prof. Gabriel 'Gabe' Roth	Maris et femmes	
Chaplin	Charlie	Calvero	Les feux de la rampe	
Cassavetes	John	Maurice Aarons	Opening Night	
Podalydès	Bruno	Michel	Comme un avion	


## Requete 15. Donnez les films de Hitchcock sans James Stewart.
localhost:3306/films/film/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=film

   Affichage des lignes 0 -  6 (total de 7, traitement en 0,0019 seconde(s).)


SELECT film.titre
FROM film
JOIN artiste AS réalisateur ON film.idRéalisateur = réalisateur.idArtiste
WHERE réalisateur.nom = 'Hitchcock' AND réalisateur.prénom = 'Alfred'
AND film.idFilm NOT IN (
    SELECT role.idFilm
    FROM role
    JOIN artiste ON role.idActeur = artiste.idArtiste
    WHERE artiste.nom = 'Stewart' AND artiste.prénom = 'James'
);


titre	
La Mort aux trousses	
Rebecca	
Les Enchaînés	
Psychose	
Les Oiseaux	
L'Inconnu du Nord-Express	
Soupçons	


## Requete 16. Dans quels films le réalisateur a-t-il le même prénom que l’un des interprètes ? (titre, nom du réalisateur, nom de l’interprète). Le réalisateur et l’interprète ne doivent pas être la même personne.
localhost:3306/films/film/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=film

   Affichage des lignes 0 -  6 (total de 7, traitement en 0,0067 seconde(s).)


SELECT film.titre, réalisateur.nom AS réalisateurNom, réalisateur.prénom AS réalisateurPrenom, acteur.nom AS acteurNom, acteur.prénom AS acteurPrenom
FROM film
JOIN artiste AS réalisateur ON film.idRéalisateur = réalisateur.idArtiste
JOIN role ON film.idFilm = role.idFilm
JOIN artiste AS acteur ON role.idActeur = acteur.idArtiste
WHERE réalisateur.prénom = acteur.prénom AND réalisateur.idArtiste != acteur.idArtiste;


titre	réalisateurNom	réalisateurPrenom	acteurNom	acteurPrenom	
Volte/Face	Woo	John	Travolta	John	
La Grande Illusion	Renoir	Jean	Gabin	Jean	
Les demoiselles de Rochefort	Demy	Jacques	Perrin	Jacques	
Les demoiselles de Rochefort	Demy	Jacques	Riberolles	Jacques	
Broken Arrow	Woo	John	Travolta	John	
Gloria	Cassavetes	John	Adames	John	
L'Armée des ombres	Melville	Jean-Pierre	Cassel	Jean-Pierre	


## Requete 17. Les films sans rôle.
localhost:3306/films/film/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=film

   Affichage des lignes 0 -  0 (total de 1, traitement en 0,0008 seconde(s).)


SELECT titre
FROM film
WHERE idFilm NOT IN (SELECT idFilm FROM role);



La Guerre des Mondes	


## Requete 18. Quelles sont les films non notés par l'internaute Prénom1 Nom1.
localhost:3306/films/film/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=film

   Affichage des lignes 0 - 24 (total de 233, traitement en 0,0035 seconde(s).)


SELECT film.titre
FROM film
WHERE idFilm NOT IN (
    SELECT notation.idFilm
    FROM notation
    JOIN internaute ON notation.email = internaute.email
    WHERE internaute.prénom = 'Prénom1' AND internaute.nom = 'Nom1'
);


titre	
La Guerre des étoiles	
Kill Bill : Volume 1	
Apocalypse Now	
Impitoyable	
Eternal Sunshine of the Spotless Mind	
A History of Violence	
2001 l'Odyssée de l'espace	
La Guerre des Mondes	
Memento	
Blade Runner	
Les Aventuriers de l'arche perdue	
Indiana Jones et le temple maudit	
Indiana Jones et la dernière croisade	
Gladiator	
Taxi Driver	
Match point	
Le Secret de Brokeback Mountain	
Breaking the Waves	
Tigre et Dragon	
Les Quatre Cents Coups	
Lost in Translation	
The Dark Knight : Le Chevalier noir	
Minority Report	
Jackie Brown	
Le Nom de la rose	


## Requete 19. Quels acteurs n’ont jamais réalisé de film ?
localhost:3306/films/artiste/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=film

   Affichage des lignes 0 - 24 (total de 986, traitement en 0,0021 seconde(s).)


SELECT artiste.nom, artiste.prénom
FROM artiste
WHERE idArtiste IN (SELECT idActeur FROM role)
AND idArtiste NOT IN (SELECT idRéalisateur FROM film);


nom	prénom	
	Bourvil	
	Terry-Thomas	
A. Fox	Vivica	
Adames	John	
Adams	Amy	
Affleck	Casey	
Aimée	Anouk	
Alexander	Jane	
Ali	Mahershala	
Allen	Joan	
Allen	Karen	
Allen	Nancy	
Altman	Allen	
Alwyn	Joe	
Amalric	Mathieu	
Amiot	Paul	
Amis	Suzy	
Anders	Glenn	
Anderson	Judith	
Anderson	Paul	
Andersson	Bibi	
Anglade	Jean-Hugues	
Ann Miller	Penelope	
Appietto	Cédric	
Arditi	Pierre	


## Requete 20. Quelle est la moyenne des notes de Memento.
localhost:3306/films/notation/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=artiste

   Affichage des lignes 0 -  0 (total de 1, traitement en 0,0017 seconde(s).)


SELECT AVG(note) AS moyenneNote
FROM notation
JOIN film ON notation.idFilm = film.idFilm
WHERE film.titre = 'Memento';



8.0000	


## Requete 21. id, nom et prénom des réalisateurs, et nombre de films qu’ils ont tournés.
localhost:3306/films/réalisateur/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=notation

   Affichage des lignes 0 - 24 (total de 107, traitement en 0,0032 seconde(s).)


SELECT réalisateur.idArtiste, réalisateur.nom, réalisateur.prénom, COUNT(film.idFilm) AS nombreFilms
FROM film
JOIN artiste AS réalisateur ON film.idRéalisateur = réalisateur.idArtiste
GROUP BY réalisateur.idArtiste, réalisateur.nom, réalisateur.prénom;


idArtiste	nom	prénom	nombreFilms	
1	Lucas	George	5	
39	Mendes	Sam	1	
40	Welles	Orson	1	
42	von Trier	Lars	2	
68	Lang	Fritz	1	
138	Tarantino	Quentin	7	
190	Eastwood	Clint	1	
201	Gondry	Michel	2	
223	González Iñárritu	Alejandro	2	
224	Cronenberg	David	4	
240	Kubrick	Stanley	7	
488	Spielberg	Steven	13	
510	Burton	Tim	1	
525	Nolan	Christopher	6	
578	Scott	Ridley	6	
638	Mann	Michael	5	
793	Buñuel	Luis	1	
1032	Scorsese	Martin	3	
1090	McTiernan	John	2	
1150	De Palma	Brian	1	
1223	Coen	Joel	2	
1224	Coen	Ethan	1	
1243	Allen	Woody	8	
1614	Lee	Ang	3	
1650	Truffaut	François	3	


## Requete 22. Nom et prénom des réalisateurs qui ont tourné au moins deux films.
localhost:3306/films/réalisateur/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=r%C3%A9alisateur

   Affichage des lignes 0 - 24 (total de 46, traitement en 0,0016 seconde(s).)


SELECT réalisateur.nom, réalisateur.prénom
FROM film
JOIN artiste AS réalisateur ON film.idRéalisateur = réalisateur.idArtiste
GROUP BY réalisateur.idArtiste, réalisateur.nom, réalisateur.prénom
HAVING COUNT(film.idFilm) >= 2;


nom	prénom	
Lucas	George	
von Trier	Lars	
Tarantino	Quentin	
Gondry	Michel	
González Iñárritu	Alejandro	
Cronenberg	David	
Kubrick	Stanley	
Spielberg	Steven	
Nolan	Christopher	
Scott	Ridley	
Mann	Michael	
Scorsese	Martin	
McTiernan	John	
Coen	Joel	
Allen	Woody	
Lee	Ang	
Truffaut	François	
Coppola	Sofia	
Ford Coppola	Francis	
Pollack	Sydney	
Hitchcock	Alfred	
Cameron	James	
Wilder	Billy	
Polanski	Roman	
Godard	Jean-Luc	


## Requete 23. Quels films ont une moyenne des notes supérieure à 7.
localhost:3306/films/film/		http://localhost/phpMyAdmin5/index.php?route=/table/sql&db=films&table=r%C3%A9alisateur

   Affichage des lignes 0 - 24 (total de 71, traitement en 0,0034 seconde(s).)


SELECT film.titre
FROM film
JOIN notation ON film.idFilm = notation.idFilm
GROUP BY film.idFilm, film.titre
HAVING AVG(notation.note) > 7;


titre	
Kill Bill : Volume 1	
Apocalypse Now	
Eternal Sunshine of the Spotless Mind	
2001 l'Odyssée de l'espace	
Memento	
Blade Runner	
Les Aventuriers de l'arche perdue	
Indiana Jones et la dernière croisade	
Gladiator	
Taxi Driver	
Lost in Translation	
The Dark Knight : Le Chevalier noir	
Minority Report	
Jackie Brown	
Terminator	
Rebecca	
Le Parrain	
Le Parrain, 2ème partie	
Le Parrain, 3ème partie	
Le Silence des Agneaux	
Jurassic Park	
Eyes Wide Shut	
Le Bateau	
Kill Bill : Volume 2	
La liste de Schindler	
