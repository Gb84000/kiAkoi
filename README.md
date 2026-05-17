# Projet kiAkoi_2026
Après analyse, il me semble plus simple de démarrer sur une application **"from scratch"**, sans s'embarrasser de l'analyse de la version antérieure **kiakoi_2022** écrite en PHP.

**Il sera fait appel aux agents I.A. tels que "Claude", "Cursor", "v0", "Copilot" et autres... afin de tester l'opportunité, l'efficacité et la pertinence de ces nouveaux outils...**

Schématiquement, **kiAkoi_2026** est  une plateforme de e-commerce, comparable à un "MarketPlace", mais accessible aux particuliers et aux professionnels, tout aussi bien pour la partie "Acheteur" que pour la partie "Vendeur". 
- **_Des particularités et services annexes <KK/> viendront se greffer au fur et à mesure de l'avancement du projet... Ils ne sont pas divulgués pour le moment. Merci de votre compréhension._**

**_L’application sera développée en localhost, puis déployée sur Internet via un hébergement VPS._**

**Elle s'appuie sur les technologies suivantes :**
- Serveur Node.js et modules tierces chargés avec "npm"
- L’applicatif est écrit en langage Javascript (et Typescript)
- De type "Fullstack", elle comporte une partie "Frontend" et une "Backend"
- Un framework "Next" associé à "React" pour la bibliothèque de composants 
- Tailwind pour le css
- Un double système de base de données hybride "mySql" et "NoSql", coté backend
- Un Cloud externe pour l'enregistrement des images
- Un "Reverse Proxy" avec "Nginx" est envisagé afin d'assurer la sécurité du projet...

**Concepts prioritaires**
- L'aspect visuel "Look & Feel" du site kiAkoi, version 2026, est prépondérant
- Une priorité sera donnée au mode "Single Page Application" et au contenu dynamique
- Des particularités et services annexes <KK/> viendront se greffer au fur et à mesure de l'avancement du projet...
<!--	Toutes les lignes balisées ainsi en début de ligne seront masquées. -->
- Une page d'accueil est conçue spécifiquement pour décrire visuellement les spécificités de la plateforme kiAkoi
- **"kiAkoi, la plateforme d'achat / vente"** est le titre (provisoire) du site Internet.
- Les services proposés par kiAkoi seront gratuits pour les particuliers. Ils seront <KK/> tarifés pour les professionnels.

## Architecture
### kiAkoi comporte deux parties distinctes mais associées : 
	Celle qui concerne un vendeur et celle qui concerne les acheteurs potentiels
Un vendeur (cf. un user_id avec un niveau d'accès et d'autorisation suffisant) saisit les informations d'un objet à vendre.
Les données de cet objet seront envoyées et stockées (et réparties) dans les bases de données kiAkoi. 

**L'enregistrement d'un objet contient :**
- L'identification unique
- L'identification unique du vendeur
- La date courante
- Un titre pour l'objet (un champ texte < 25 caractères)
- La catégorisation de l'objet (la plateforme propose une douzaine de catégories distinctes, ainsi que des sub-catégories). (voir categories)
- Un descriptif détaillé (lequel doit s'adapter selon la catégorie). (2048 caractères maxi enregistrés en BDD noSql...).
- Un résumé automatiquement élaboré (limité à 256 caractères) à partir du descriptif saisi par le vendeur
- Une à 9 photos, uploadées au gré du vendeur (enregistrées en Cloud externe)
- Un champ pour l'état de l'objet (neuf ou non, excellent, très bon état, moyen, etc...) 
	
Plusieurs autres enregistrements (également avec l'association objet/vendeur) recensent d'autres informations évolutives :
- La quantité d'objets identiques disponibles à une date courante
- La localisation géographique de l'objet
- Le mode de livraison
- Le prix demandé et le mode de paiement

**Après validation par le vendeur, puis vérifiée par un modérateur, l'annonce est publiée sur le site kiAkoi.**
 
**Les utilisateurs (même non enregistrés) qui visitent le site peuvent consulter et rechercher librement les annonces publiées ...** 
Ils disposent de plusieurs outils de tri et de sélections pour la recherche ciblée des objets
- Selection par catégorie, par prix, par périmètre géographique, par mots-clés, par date de création
- Selon la catégorisation, des champs de recherche complémentaires peuvent être proposés

La visualisation des objets est à deux niveaux : 
- Le niveau "Resume" avec une photo principale de l'objet, ainsi que le résumé et le prix.
_```(Ce mode de visualisation permet la navigation aisée et rapide entre plusieurs objets précédemment ciblés par la sélection)```_
- Le niveau "Details" permet de focaliser sur une page toutes les informations spécifiques à un objet et notamment la visualisation des différentes photos

**Les visiteurs doivent cependant être enregistrés et autorisés pour accéder à des fonctionnalités supplémentaires réservées aux "Membres"**
(cf. un user_id avec un niveau d'accès et d'autorisation suffisant). Il peut approfondir sa visite en tant qu'acheteur potentiel.
	Lors de sa consultation, l'acheteur potentiel peut "marquer" les objets afin de les retrouver ultérieurement (marquage "favori") ou les supprimer
	Le dialogue et une messagerie <KK/> entre l'acheteur et le vendeur viendront se greffer ultérieurement au projet.
	
Le site kiAkoi mettra en place <KK/> une évaluation des "Membres" acheteurs et/ou vendeurs 
Un historique <KK/> permettra de recenser les transactions effectuées par chacun des Membres

## Identification
Concernant les "Membres", leurs informations personnelles et leurs niveaux d'accès sont enregistrés dans la base de données Sql :
| Champ      |   val   | Description                                                                                                                                                                                         |
| :--------- | :-----: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| member_id  |         | Identification unique                                                                                                                                                                               |
| email      |         | Adresse email validée                                                                                                                                                                               |
| mdp        |         | Mot de passe crypté                                                                                                                                                                                 |
| pseudo     |         | unique, le système proposera éventuellement un suffixe _numérique, par exemple "Mon-pseudo_123"                                                                                                     |
| vip        |   "V"   | Visiteur, sans identification, pour une simple visite, sans aucun cookies de mémorisation. Accès limité. Permet de voir le site, son architecture et ce qu'il propose... Objets, Catégories, etc... |  |
|            |         | A noter : "V" est attribué par défaut avant une phase systématique de vérification de l'adresse email                                                                                               |
|            |   "I"   | Identifié par son adresse email et un mot de passe. Les visites sont mémorisées, et l'accès est étendu.                                                                                             |
|            |   "P"   | Personnalisé par son Pseudo et ses données personnelles. Niveau nécessaire pour accéder à toutes les fonctionnalités  (en coordination avec le champ card_3G).                                      |
| card_3G    |   ""    | No card                                                                                                                                                                                             |
|            | "Grey"  | Grey card, accès de base                                                                                                                                                                            |
|            | "Green" | Green card, accès supérieur                                                                                                                                                                         |
|            | "Gold"  | Gold card, accès prioritaire                                                                                                                                                                        |
| stars      |   "*"   | Evaluation (1 à 5 étoiles)                                                                                                                                                                          |  |
| adresse    |         | Adresse... Ville... Téléphone... Pays                                                                                                                                                               |
| date_in       |         | Date d'inscription                                                                                                                                                                                  |  |
| date_off |         | Date de désinscription                                                                                                                                                                              |


## Les "Catégories" : A suivre...

## Le moteur de recherche par mots-clés...

**Ce document est la version 1.0.0.  Si ce projet 2026 vous interesse, ainsi que son évolution au fil des mois, merci de vous faire connaître... gerald.bayart@gmail.com**
