fiche technique:

## Description

Cette API est un exemple de base pour une API RESTful qui permet de créer, lire, mettre à jour et supprimer des utilisateurs. Elle est écrite en Python à l'aide du framework FastAPI et utilise une base de données SQLite pour stocker les informations des utilisateurs.

## Fonctionnalités

L'API expose les endpoints suivants :

- `POST /users/` : crée un nouvel utilisateur avec les détails fournis dans le corps de la requête
- `GET /users/` : renvoie tous les utilisateurs enregistrés dans la base de données
- `GET /users/{user_id}` : renvoie les détails d'un utilisateur spécifique en fonction de son ID
- `PUT /users/{user_id}` : met à jour les détails d'un utilisateur existant en fonction de son ID et des détails fournis dans le corps de la requête
- `DELETE /users/{user_id}` : supprime un utilisateur existant en fonction de son ID

Les données des utilisateurs sont stockées dans une base de données SQLite. Les détails des utilisateurs sont définis par un modèle Pydantic appelé `User`.

## Dépendances

Les dépendances suivantes sont nécessaires pour exécuter cette API :

- Python 3.7 ou supérieur
- FastAPI
- Uvicorn
- Pydantic
- SQLite3

## Utilisation

1. Clonez le dépôt GitHub : `git clone https://github.com/Aichael29/FastAPI_Training/tree/AE_FastApi_users_information`
2. Installez les dépendances : `pip install -r requirements.txt`
3. Exécutez le serveur : `uvicorn main:app --reload`
4. Accédez à l'API à l'adresse http://localhost:8000/docs pour consulter la documentation et tester les différents endpoints à l'aide de l'interface Swagger UI.
