## FastAPI_GenAno
Le code fourni est un serveur FastAPI permettant de générer des nombres aléatoires , de les stocker dans un fichier CSV et chiffrer ou déchiffrer les données d'un fichier CSV . 

Utilisez un terminal pour vous rendre dans le répertoire du projet et exécuter la commande suivante:
* uvicorn main:app --reload

maintenant Vous pouvez tester tous les routes disponibles en utilisant Postman
### Les routes disponibles sont:
*  ### /: `renvoie un message de salutation`
* Vous pouvez le tester en utilisant Postman:
1.	Ouvrez Postman et créez une nouvelle requête GET.
2.	Dans l'URL de la requête, entrez l'URL de l'API que vous avez créée. Par exemple, si votre API est hébergée localement sur le port 8000, l'URL sera http://localhost:8000/.
3.	Cliquez sur le bouton "Send" pour envoyer la requête GET à l'API.
Vous devriez maintenant voir une réponse de l'API dans Postman. La réponse devrait être un objet JSON contenant une propriété "greeting" avec la valeur "Hello world".


*  ### POST /generate:`génère un nombre spécifié de nombres aléatoires entre une valeur minimale et maximale spécifiée, renvoyant les données générées au format JSON`
* Vous pouvez le tester en utilisant Postman:
1.	Ouvrez Postman et créez une nouvelle requête POST.
2.	Dans l'URL de la requête, entrez l'URL de l'API que vous avez créée, suivi de "/generate". Par exemple, si votre API est hébergée localement sur le port 8000, l'URL sera http://localhost:8000/generate.
3.	Cliquez sur l'onglet "Body" dans Postman, puis sélectionnez "raw" et "JSON" dans le menu déroulant.
4.	Dans le corps de la requête, entrez un objet JSON qui contient les propriétés "count", "min_value" et "max_value". Par exemple :
{
"count": 10,
"min_value": 0,
"max_value": 100
}
Cela indique à l'API de générer 10 nombres aléatoires entre 0 et 100 inclus.
5.	Cliquez sur le bouton "Send" pour envoyer la requête POST à l'API.
Vous devriez maintenant voir une réponse de l'API dans Postman. La réponse devrait être un objet JSON contenant une propriété "data" avec une liste de nombres aléatoires générés

* ### POST /generate_and_store: ` Cette fonctiongénère des données aléatoires pour les colonnes spécifiées et les enregistre dans un fichier CSV.`
Vous pouvez le tester en utilisant Postman:
1. Assurez-vous que votre serveur est en cours d'exécution et que vous avez accès à l'URL de l'API. 
2. Ouvrez Postman et créez une nouvelle requête POST. 
3. Entrez l'URL de l'API, par exemple http://localhost:8000/generate_and_store si vous exécutez l'API localement. 
4. Cliquez sur l'onglet "Body" et sélectionnez "JSON" comme type de contenu. 
5. Dans le corps de la requête, entrez les informations de la demande en JSON. Par exemple :
{
    "num_rows": 10,
    "file_path": "C:/Users/pc/Desktop/stage_inwi/random_data.csv",
    "column_types": {
        "id": "int",
        "name": "str",
        "age": "int",
        "is_student": "bool"
    }
}
Ceci est un exemple de demande pour générer 100 lignes de données aléatoires avec quatre colonnes : "id", "name", "age", "is_student"
6. Appuyez sur le bouton "Envoyer" pour envoyer la demande à l'API. 
7. La réponse de l'API devrait apparaître dans le volet de droite de Postman. Si les données ont été générées avec succès, vous devriez voir un message indiquant que les données ont été enregistrées dans le fichier spécifié(par defaut path=C:/Users/pc/Desktop/stage_inwi/random_data.csv). Sinon, vous verrez un message d'erreur.
Vous pouvez également vérifier que les données ont été enregistrées dans le fichier en ouvrant le fichier "random_data.csv" avec un éditeur de texte ou un tableur.
*   ### PUT /update: `la fonction met à jour les valeurs de la "line_number" ligne à l'aide du dictionnaire "new_values".`
* Vous pouvez le tester en utilisant Postman:
1.	Ouvrir Postman et créer une nouvelle requête PUT. 
2. Dans l'URL, spécifiez l'URL correspondant à la route "/update" de votre application. 
3. Dans le corps de la requête, sélectionnez "form-data" comme type de données et ajoutez les clés et valeurs suivantes :
"file_path" : spécifiez le chemin d'accès au fichier CSV que vous souhaitez mettre à jour.
"line_number" : spécifiez le numéro de ligne dans le fichier que vous souhaitez mettre à jour.
"new_values" : spécifiez les nouvelles valeurs que vous souhaitez mettre à jour pour cette ligne, sous forme de dictionnaire JSON,exemple:
{
    "file_path": "C:/Users/pc/Desktop/stage_inwi/random_data.csv",
    "line_number": 2,
    "new_values": {
       "id": 100,
        "name": "azerty",
        "age": 20,
        "is_student": "False"
        
    }
}
4. Cliquez sur le bouton "Send" pour envoyer la requête PUT à l'API.
Si la requête est traitée avec succès, vous devriez voir une réponse avec un message indiquant que la ligne spécifiée a été mise à jour dans le fichier CSV spécifié. Si la requête échoue pour une raison quelconque, vous devriez voir une erreur correspondante dans la réponse
*  ### DELETE /delete: `supprime une ligne spécifiée d'un fichier CSV.`
* Vous pouvez  le tester en utilisant Postman:
1.	Ouvrir Postman et créer une nouvelle requête DELETE.
2.	Ajouter l'URL de l'API dans la barre d'adresse, par exemple http://localhost:8000/delete.
3. Dans le corps de la requête, entrez un objet JSON qui contient les propriétés  "file_path"(path de fichier qu'on veut supprimé)et "line_number"(le numéro de la ligne à supprimer). Par exemple :
{
    "file_path": "C:/Users/pc/Desktop/stage_inwi/random_data.csv",
    "line_number": 2
}
4. Envoyer la requête et vérifier que la réponse contient le message "Ligne 2 supprimée avec succès!".
Vérifier que le fichier CSV a bien été mis à jour en utilisant un éditeur de texte.

* ### POST /encrypt_file: `chiffrer ou déchiffrer les données d'un fichier CSV en utilisant l'algorithme AES-256-CBC ou de hasher les données en utilisant l'algorithme SHA256. L'API prend en entrée le chemin du fichier source, le chemin du fichier de sortie, l'opération à effectuer (chiffrement, déchiffrement ou hashage), la clé de chiffrement, le mode de chiffrement, le vecteur d'initialisation, les colonnes à chiffrer/déchiffrer (optionnel), le séparateur de champ (optionnel) et retourne le fichier de sortie modifié.`
* Vous pouvez le tester en utilisant Postman:
1.	Ouvrir Postman et créer une nouvelle requête POST.
2.	Ajouter l'URL de l'API dans la barre d'adresse, par exemple http://localhost:8000/encrypt_file.
3.	Ajouter un corps de requête de type JSON contenant les paramètres d'entrée pour la fonction, par exemple :
{
    "fichier_entree": "C:/Users/pc/Desktop/stage_inwi/data.csv",
    "fichier_sortie": "C:/Users/pc/Desktop/stage_inwi/dataDA1.csv",
    "operation": "chiffrement",
    "cle_chiffrement": "ma_cle_secrete12",
    "mode_chiffrement": "CBC",
    "vecteur": "monvecteursecret",
    "colonnes": "id",
    "separateur": ";"

}
4.	Envoyer la requête et vérifier que la réponse contient le message "Fichier encrypté avec succès!".
Vérifier que le fichier de sortie a été créé avec les données modifiées en utilisant un éditeur de texte ou en répétant la lecture du fichier avec un script Python.

* ### Le code importe également les modules random et csv, ainsi que le module fct (contient les fct de chiffrement,dechiffrement et hachage), et définit les modèles de données RandomData et RandomData1 à l'aide de la bibliothèque Pydantic.