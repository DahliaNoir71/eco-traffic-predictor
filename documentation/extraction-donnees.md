📄 Spécifications Techniques : Module d'Extraction de Données
Projet : Eco-Traffic Predictor Version : 1.0 Responsable : [Ton Nom]

1. Présentation du Module
Ce module a pour but d'automatiser la récupération de données brutes depuis des sources hétérogènes pour alimenter le lac de données (Data Lake) du projet. Il doit garantir la pérennité de la collecte et gérer les pannes potentielles des sources externes.

2. Inventaire des Sources et Contraintes Techniques
Le script devra se connecter aux 5 types de sources exigés par le référentiel .

A. Source Web Service (API REST) : Données Météorologiques
Source : OpenWeatherMap (ou équivalent).

Données : Température, humidité, vent (format JSON).

Contraintes Techniques :

Authentification : Nécessite une clé API (API_KEY) qui ne doit pas être codée en dur (sécurité).

Quota (Rate Limiting) : Limitation à 60 appels/minute (version gratuite). Le script doit gérer un temps d'attente si nécessaire.

Protocole : HTTP/1.1 via méthode GET.

B. Source Web Scraping : Alertes Trafic
Source : Site web d'info trafic (ex: Page HTML simulée ou Bison Futé).

Données : Liste des incidents, localisation, heures (format HTML).

Contraintes Techniques :

Structure DOM : Les données sont imbriquées dans des balises <div> avec des classes CSS spécifiques (ex: .traffic-alert). Une modification du site cassera le script (fragilité).

Légalité : Respect du fichier robots.txt et des conditions d'utilisation du site.

Parsing : Nécessite un parseur HTML robuste (ex: BeautifulSoup ou lxml).

C. Source Fichier Plat : Référentiel Capteurs
Source : Fichier statique capteurs_air.csv (simulé Data.gouv).

Données : ID capteur, coordonnées GPS, type de gaz.

Contraintes Techniques :

Encodage : Risque de conflit UTF-8 vs Latin-1 (ISO-8859-1).

Délimiteur : Vérifier si le séparateur est une virgule , ou un point-virgule ;.

Chemin d'accès : Le chemin doit être relatif pour fonctionner sur n'importe quelle machine clonant le dépôt Git.

D. Source Base de Données (SGBDR) : Utilisateurs & Zones
Source : Base PostgreSQL (CRM simulé).

Données : ID Utilisateur, email (donnée personnelle), zone géographique préférée.

Contraintes Techniques :

Sécurité : Les identifiants (Host, User, Pwd, Port) doivent être externalisés.

Connectivité : Le script doit gérer les interruptions réseau (Timeouts).

RGPD : Les données extraites contiennent des PII (Personal Identifiable Information) et doivent être sécurisées dès l'extraction.

E. Source Big Data : Historique de Trafic
Source : Cluster Hadoop/Hive (simulé via Docker).

Données : Moyennes de trafic agrégées sur 5 ans (Volumétrie importante).

Contraintes Techniques :

Latence : Les requêtes Hive peuvent être lentes à démarrer (MapReduce/Tez).

Driver : Nécessite un connecteur spécifique compatible Python (ex: PyHive ou Thrift).

3. Architecture du Script d'Extraction
Pour valider les critères de qualité , le script sera structuré de manière modulaire.

3.1 Structure des Fichiers
Plaintext

project_root/
├── .env                 # Variables d'environnement (Clés API, Mots de passe) - Non versionné
├── requirements.txt     # Dépendances
├── data/
│   └── raw/             # Dossier de réception des données brutes (Landing Zone)
├── logs/                # Fichiers journaux d'exécution
└── src/
    ├── main.py          # Point d'entrée unique (Orchestrateur)
    ├── config.py        # Chargement de la configuration
    └── extractors/      # Modules spécifiques
        ├── api_weather.py
        ├── scraper_traffic.py
        ├── db_users.py
        ├── file_sensors.py
        └── bigdata_history.py
3.2 Algorithme Principal (main.py)
Le flux d'exécution suivra strictement ces étapes :

Initialisation :

Chargement des variables depuis .env.

Création des répertoires data/raw et logs si inexistants.

Initialisation du Logger (format : [DATE] [LEVEL] Message).

Exécution Séquentielle (Orchestration) :

Le script appelle successivement les fonctions extract() de chaque module.

Gestion des Erreurs (Error Handling) :

Utilisation de blocs try...except pour chaque source.

En cas d'échec d'une source (ex: API météo hors ligne), le script loggue l'erreur mais continue pour les autres sources (Fail-safe).

Sauvegarde (Persistance) :

Chaque module sauvegarde ses données brutes immédiatement dans data/raw/ avec un nom horodaté (ex: weather_2023-10-27.json).

Finalisation :

Fermeture propre des connexions BDD.

Log de fin de traitement.

3.3 Dépendances Techniques (Stack)
requests : Pour les appels API HTTP .

pandas : Pour la manipulation et lecture CSV/Excel .

beautifulsoup4 : Pour le scraping HTML .

sqlalchemy / psycopg2 : Pour la connexion PostgreSQL .

python-dotenv : Pour la sécurité des configurations.

✅ Validation des Critères pour cette étape :
Identification des contraintes : Listées pour chaque source (Section 2).

Script structuré : Architecture définie avec point de lancement et gestion erreurs (Section 3).

Sécurité : Mention de l'exclusion des mots de passe du code source.