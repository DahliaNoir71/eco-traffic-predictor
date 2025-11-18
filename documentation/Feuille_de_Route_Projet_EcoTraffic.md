🗺️ Feuille de Route du Projet : Eco-Traffic Predictor
Objectif : Validation du Titre "Développeur en Intelligence Artificielle" - Bloc A1 & A2 (Data Engineering).


Contexte : Mise en place d'un pipeline de données pour un service IA de prédiction de la qualité de l'air.

📅 Phase 1 : Cadrage et Environnement Technique
Objectif : Mettre en place les fondations du projet et les outils de collaboration.

1.1. Initialisation du Dépôt Git

Créer un dépôt (GitHub/GitLab) pour héberger le projet.


Mettre en place un fichier .gitignore (pour exclure les données brutes, les fichiers .env et les caches).

Créer le fichier requirements.txt pour gérer les dépendances Python.

1.2. Rédaction des Spécifications Techniques (Extraction)

Rédiger un document listant les contraintes techniques des sources (API, Web, BDD).


Définir l'architecture du script d'extraction (point d'entrée, gestion erreurs).


📥 Phase 2 : Développement du Module de Collecte (Compétences A1 / C1 & C2)

Objectif : Automatiser l'extraction de données depuis 5 sources hétérogènes.


2.1. Connexion API REST (Météo)

Développer une fonction Python pour requêter l'API OpenWeatherMap.


Gérer l'authentification (API Key) et récupérer le format JSON.

2.2. Web Scraping (Alertes Trafic)

Développer un script (BeautifulSoup/Selenium) pour télécharger le HTML d'un site d'info trafic.


Parser le HTML pour extraire les incidents en cours.


2.3. Lecture de Fichiers (Capteurs)

Implémenter la lecture automatique d'un fichier CSV/Excel contenant les positions des capteurs.


2.4. Base de Données & Big Data (Historique & Utilisateurs)

Configurer un conteneur Docker avec une base SQL (PostgreSQL) et un système Big Data simulé (Hive/Spark).



Livrable C2 : Écrire et documenter des requêtes SQL complexes (jointures, agrégations) pour extraire les données pertinentes.


Documenter les optimisations choisies pour ces requêtes.


2.5. Finalisation du Script de Collecte

Assembler les fonctions dans un script unique, robuste, avec gestion des exceptions et logs.


🧹 Phase 3 : Agrégation et Nettoyage (Compétence C3)

Objectif : Créer un jeu de données unique, propre et homogène.

3.1. Spécifications de Nettoyage

Définir les règles de gestion des erreurs (ex: suppression des valeurs nulles ou aberrantes).


3.2. Développement du Script de Transformation

Programmer la détection et suppression des entrées corrompues.



Homogénéiser les formats (dates en ISO 8601, unités métriques unifiées).


Fusionner les données (Météo + Trafic + Capteurs) en un seul DataFrame/Fichier.

3.3. Documentation

Documenter l'algorithme de nettoyage et les choix effectués.


💾 Phase 4 : Stockage et Conformité RGPD (Compétence A2 / C4)

Objectif : Stocker les données propres dans une base structurée et légale.

4.1. Modélisation des Données (Merise)

Réaliser le Modèle Conceptuel de Données (MCD) et le Modèle Logique (MLD).


Intégrer les tables : Mesures, Capteurs, Incidents, Utilisateurs.

4.2. Installation et Création de la BDD

Choisir et installer le SGBD (ex: PostgreSQL).


Implémenter le script de création des tables (DDL).


4.3. Conformité RGPD

Rédiger le registre des traitements pour les données "Utilisateurs".


Écrire une procédure de tri/suppression des données personnelles obsolètes.


4.4. Import des Données

Développer le script d'import pour insérer le jeu de données nettoyé (Phase 3) dans la BDD.


🔌 Phase 5 : Mise à disposition via API (Compétence C5)

Objectif : Exposer les données via une architecture REST sécurisée.

5.1. Configuration de l'API

Initialiser le projet API (Framework : FastAPI ou Flask).


5.2. Développement des Endpoints

Créer les routes (GET/POST) pour accéder aux prédictions et alertes.


Connecter l'API à la base de données créée en Phase 4.

5.3. Sécurisation

Mettre en place un système d'authentification (Token ou API Key).


Appliquer les bonnes pratiques de sécurité (validation des entrées).

5.4. Documentation API

Générer la documentation technique (Swagger/OpenAPI) décrivant les points de terminaison.


📝 Phase 6 : Livrables Finaux et Soutenance
Vérifier que tous les scripts sont versionnés sur Git.

Compiler le Rapport Professionnel incluant les spécifications, les modèles Merise, le registre RGPD et la documentation API.


Préparer la soutenance orale.