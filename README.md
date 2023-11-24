# PostgreSQL
--créer une table de données fiche clients : 
CREATE TABLE fiche_clients (
    id SERIAL PRIMARY KEY,
    nom VARCHAR(50),
    prenom VARCHAR(50),
    date_naissance DATE,
    age INTEGER,
    code_postal VARCHAR(10),
    ville VARCHAR(50),
    numero_contrat VARCHAR(20)
);

--Remplir aléatoirement cette table avec generate series : 
INSERT INTO nouvelle_fiche_clients (nom, prenom, date_naissance, age, code_postal,
 ville, numero_contrat)
SELECT
    -- Générer un nom aléatoire
    'Nom' || floor(random() * 1000)::int,
    
    -- Générer un prénom aléatoire
    'Prenom' || floor(random() * 1000)::int,
    
    -- Générer une date de naissance aléatoire dans les 30 dernières années
    CURRENT_DATE - INTERVAL '1 day' * floor(random() * 365 * 30),
    
    -- Générer un âge aléatoire entre 18 et 80 ans
    floor(random() * (80 - 18 + 1)) + 18,
    
    -- Générer un code postal aléatoire
    floor(random() * 90000 + 10000)::int,
    
    -- Générer une ville aléatoire
    'Ville' || floor(random() * 1000)::int,
    
    -- Générer un numéro de contrat aléatoire
    'Contrat' || floor(random() * 100000)::int
FROM generate_series(1, 200);  -- Générer 200 lignes

--Visualiser mon tableau : 
select * from nouvelle_fiche_clients;

Nous remarquons que dans notre tableau, les colonnes noms et prénoms ne sont pas bien
 générées.
En effet, PostgreSQL ne fournit pas de générateur de noms/prénoms intégré, mais nous 
pouvons créer notre propre table de référence et l'utiliser dans nos requêtes.

Pour cela, il faudra créer une nouvelle table:
Create table nom_prénom_référence (
nom varchar (50), prenom varchar (50));
Je vais créer la nouvelle table dans un autre fichier.(syntaxe+donées)
