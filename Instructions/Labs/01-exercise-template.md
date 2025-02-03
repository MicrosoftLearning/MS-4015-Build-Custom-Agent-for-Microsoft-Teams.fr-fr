
Labo : « Créer un agent personnalisé »
---
<!--
Edit the metadata above to manage the list of exercises in the home page of the GitHub site that gets generated.
You can delete the module and edit index.md in the root of the repo to customize the display so that only the exercises are listed
To enable GitHub page publishing, edit the Page settings for the repo and publish from the main branch
-->

# Créer et tester un agent personnalisé

Dans cet exercice, vous allez créer une ressource Azure OpenAI qui sert de base à la création de votre agent personnalisé.

Cet exercice devrait prendre environ **30** minutes. <!-- update with estimated duration -->

**Remarque :** les apprenants sont censés terminer ce laboratoire sur leurs propres environnements.

##  Tâche 1 : créer une ressource Azure OpenAI 

En premier lieu, vous devez...

1. Dans votre navigateur Edge, accédez à **https://portal.azure.com**.
1. Connectez-vous au portail Azure.
2. Dans le coin supérieur gauche de l’écran, cliquez sur **+ Créer une ressource**.
1. Dans la zone de recherche, tapez **Azure OpenAI**, appuyez sur Entrée.
1. Un résultat appelé **Azure OpenAI** doit apparaître en tant qu’option. En bas à gauche de cette option, un bouton intitulé **Créer** est affiché. Appuyez sur > **Créer** > Azure **OpenAI**.
1. Dans la page **Créer Azure OpenAI**, définissez les champs suivants : **Remarque : **comme ce labo est censé être effectué sur le propre environnement des apprenants, ceux-ci devront faire preuve de discernement pour sélectionner les valeurs des champs **Abonnement**, **Niveau tarifaire** et **Groupe de ressources**.
   
   a. **Abonnement** : faites preuves de discernement pour remplir ce champ.
   
   b. **Groupe de ressources** : faites preuve de discernement pour remplir ce champ.
   
   c. **Nom** : tapez un nom de votre choix.
   
   d. **Niveau tarifaire** : la valeur par défaut est **Standard S0**, mais faites preuve de discernement pour remplir ce champ.
   
Cliquez sur **Suivant**.

7. Sur la page suivante, dans l’onglet **Réseau** , sélectionnez l’option **Tous les réseaux, y compris Internet, peuvent accéder à cette ressource**.
Cliquez sur **Suivant**.
8. Sur la page suivante, dans l’onglet **Balises**, laissez les champs Nom et Valeur vides.
Cliquez sur **Suivant**.
9. Sur la page suivante, dans l’onglet **Vérifier et envoyer**, appuyez sur **Créer**.
10. Vous serez redirigé vers une page dans laquelle cette ressource Azure OpenAI nouvellement créée est en cours de création. **Déploiement en cours** s’affichera. Attendez la fin du déploiement de cette ressource. Cela prendra quelques secondes. Une fois la ressource déployée, cliquez sur le bouton **Accéder à la ressource**.
11. **Résultat :** vous serez maintenant sur la page avec la ressource Azure OpenAI nouvellement créée. Vous pouvez vérifier en cherchant le nom de la ressource dans le coin supérieur gauche de la page. Ce nom doit correspondre au nom que vous avez choisi à l’étape 5c ci-dessus.


## Tâche 2 : implémenter la RAG pour le modèle Azure OpenAI

Dans cette tâche, vous allez apprendre à implémenter la RAG à l’aide d’une source de données pour votre propre environnement de test.

1. Dans la page de votre ressource Azure OpenAI nouvellement créée, dans le ruban en haut de la page, cliquez sur **Accéder à Azure AI Foundry**.
2. Dans la nouvelle page intitulée **Terrain de jeu de conversation**, dans **Configuration**, sélectionnez **+ Créer un déploiement** > **À partir de modèles de base**.
3. Dans la fenêtre contextuelle intitulée **Sélectionner un modèle de saisie semi-automatique de la conversation**, faites défiler vers le bas et sélectionnez l’option **gpt-4o** > **Confirmer**.
4. Dans la fenêtre **Déployer le modèle gtp-4o**, laissez tout ses paramètres par défaut, puis sélectionnez **Déployer**.
5. Dans la page **Terrain de jeu de conversation**, en bas de l’écran, sélectionnez **Ajouter vos données** > **+ Ajouter une source de données**.
6. Dans la fenêtre **Sélectionner ou ajouter une source de données**, sélectionnez **Sélectionner une source de données** dans la liste déroulante, puis **Charger des fichiers (préversion)**.
7. Dans la page suivante pour **Source de données**, vérifiez que la liste déroulante pour **Sélectionner une source de données** est définie sur **Charger des fichiers (préversion)**.
   
   a. Dans le champ **Abonnement**, vérifiez que la valeur par défaut est sélectionnée.
   
    b. Dans le champ **Sélectionner une ressource de stockage Blob Azure**, sélectionnez **Créer une ressource de stockage Blob Azure** > dans la nouvelle fenêtre intitulée **Créer un compte** de stockage, dans l’onglet **Informations de base**, vérifiez que les champs **Abonnement** et **Groupe de ressources** sont définis sur les valeurs par défaut. Choisissez la seule valeur disponible pour **Groupe de ressources**. Dans **Détails de l’instance**, indiquez un nom pour **Nom de compte de stockage**. Laissez le reste des champs tels quels. Sélectionnez **Revoir + créer**. Dans l’onglet **Examiner et créer**, sélectionnez le bouton **Créer**. Le déploiement de la ressource Stockage Blob Azure prend quelques instants.
   
   c. Revenez à la fenêtre **Terrain de jeu de conversation**. Sélectionnez le bouton Actualiser en regard du champ **Sélectionner la ressource Stockage Blob Azure** > sélectionnez la ressource que vous avez créée à l’étape b ci-dessus. Sélectionnez le bouton **Activer CORS**.
   
8. Pour le champ **Sélectionner une ressource Recherche Azure AI**, sélectionnez **Créer une ressource Recherche Azure AI**.  Vérifiez que les champs **Abonnement** et **Groupe de ressources** sont définis sur les valeurs de votre choix.

   **Remarque :** étant donné que ce labo est destiné à être effectué sur le propre environnement des apprenants, ceux-ci devront faire preuve de discernement pour sélectionner les valeurs des champs **Abonnement** et **Groupe de ressources**.

9. Cliquez sur la liste déroulante **Groupe de ressources** pour sélectionner l’option de votre choix. Entrez un **nom de service** > vérifiez que tous les autres champs sont définis sur les valeurs par défaut > sélectionnez **Examiner et créer** > **Créer**. Le déploiement de la ressource Recherche Azure AI prend quelques instants.
10. Revenez à la fenêtre **Terrain de jeu de conversation**. Sélectionnez le bouton Actualiser en regard du champ **Sélectionner la ressource Stockage Blob Azure** > sélectionnez la ressource que vous avez créée à l’étape 9 ci-dessus.
11. Entrez un nom pour le champ **Entrer le nom de l’index** > **Suivant**. Copiez et collez ce nom dans un endroit accessible, car vous en aurez besoin dans les tâches à venir.
12. Dans la section **Charger des fichiers**, sélectionnez **Parcourir un fichier** > dans l’Explorateur de fichiers, accédez à **Documents** > sélectionnez les trois fichiers : **ContosoAI ChipEnhance Perks Program.docx**, **ContosoAI Insurance Plans.docx** et **Overview of ContosoAI.docx** > **Ouvrir** > les trois fichiers doivent maintenant se trouver dans la page **Charger les fichiers** de la fenêtre > sélectionnez **Charger des fichiers** > **Suivant**.
13. Dans la section **Gestion des données**, laissez toutes les valeurs par défaut, puis sélectionnez **Suivant**.
14. Dans **Connexion de données**, sélectionnez **Clé API** > **Suivant** > **Enregistrer et fermer**.
15. Dans la fenêtre **Terrain de conversation de conversation**, sélectionnez **Afficher le code** qui se trouve dans le ruban en haut à gauche de la fenêtre.
16. Dans la fenêtre **Exemple de code**, sélectionnez la liste déroulante à droite du premier champ, puis sélectionnez **JSON** > basculez vers l’onglet **Authentification de clé ** :
    
    a. Copiez et collez les valeurs suivantes, car vous en aurez besoin dans les tâches à venir : **point de terminaison**, **clé API** et **clé de ressource Recherche Azure**. Vous pouvez également laisser cette fenêtre ouverte pour collecter ces valeurs pour les tâches à venir.

 ## Tâche 3 : créer et tester un agent personnalisé dans l’outil de test et Teams

Dans cette tâche, vous allez créer l’agent personnalisé et le tester.

1. Ouvrez **Visual Studio Code**.
2. Dans la partie droite de la fenêtre Visual Studio Code, sélectionnez l’icône **Teams Toolkit** > sélectionnez **Create a New App** > dans la liste déroulante, sélectionnez **Custom Engine Agent** (remarque : selon la version de Teams Toolkit, vous devrez peut-être sélectionner **Custom Copilot**) > **Basic AI Chatbot** > **JavaScript** > **Azure OpenAI**.
3. Dans la zone vide située en haut de l’écran, entrez d’abord :

   a. **Clé API** de la tâche précédente > **Entrée**.

   b. **Point de terminaison** de la tâche précédente > **Entrée**.

   c. Pour **Azure Open AI deployment name**, tapez **gpt-4o** > **Entrée**.

   d. Pour **Choose the folder where your project room folder will be located**, sélectionnez **Default folder**.

   e. Pour **Input application name**, tapez un nom > **Entrée**> dans la fenêtre contextuelle, sélectionnez **Yes, I trust the authors**.

   f. Dans la nouvelle fenêtre VS Code de l’application créée à partir des étapes a-f ci-dessus, accédez à l’icône **Teams Toolkit** sur le côté gauche de l’écran.

   **Remarque :** les étapes g-i doivent être effectuées pour l’environnement d’un utilisateur qui n’a pas d’accès administrateur au Centre d’administration Microsoft Teams. Si les utilisateurs disposent d’un locataire M365 avec l’accès administrateur, effectuez les étapes j-m à la place.

   g. Dans la section **Accounts**, cliquez sur **Sign in to Microsoft 365**. Cela ouvrira une nouvelle fenêtre dans le navigateur. Connectez-vous à l’aide des informations d’identification fournies.

   .h Revenez à la page VS Code de votre application. Vous devez maintenant voir une coche verte à côté des mots **Custom App Upload Enabled** dans **Accounts.

   i. Dans la section **Accounts**, cliquez sur **Sign in to Azure**. Cliquez sur **OK** dans chaque fenêtre contextuelle. Cela ouvrira une nouvelle fenêtre dans le navigateur. Connectez-vous à l’aide des informations d’identification fournies.

   Pour les utilisateurs disposant d’un locataire M365 avec un accès administrateur au Centre d’administration Microsoft Teams, effectuez les étapes suivantes au lieu des étapes g-i ci-dessus :

   j. Connectez-vous à https://admin.teams.microsoft.com avec vos informations d’identification d’administrateur.

   k. Accédez aux  **applications Teams**  dans la barre latérale, puis sélectionnez  **Stratégies de configuration**.

   l. Sélectionnez la stratégie  **globale (valeur par défaut à l’échelle de l’organisation)** , puis activez le bouton bascule  **Charger des applications personnalisées** .

   m. Faites défiler vers le bas et sélectionnez le bouton  **Enregistrer**  pour enregistrer les modifications. Votre locataire autorise désormais le chargement indépendant d’applications personnalisées. 
   
5. Accédez à **src/prompts/chat/skprompt.txt** dans la fenêtre VS Code de votre application. Supprimez le texte du fichier et collez ce qui suit : « Delete any text in the file and paste the following: "The following is a conversation with an AI assistant, who is an expert on answering questions over the given context. 

Responses should be in a short journalistic style with no more than 80 words. » 

5. Accédez au fichier **config.json** sous les prompts/chat dans la fenêtre VS Code de votre application. Supprimez le code actuellement présent entre crochets et collez le code suivant entre crochets.

```json
"data_sources": [ 
    { 
        "type": "azure_search", 
        "parameters": { 
            "endpoint": "AZURE-AI-SEARCH-ENDPOINT", 
            "index_name": "YOUR-INDEX_NAME",
            "in_scope": false,
            "authentication": { 
                "type": "api_key", 
                "key": "AZURE-AI-SEARCH-KEY" 
            } 
        } 
    } 
]
```

6. Dans le code ci-dessus, remplacez ce qui suit par les valeurs que vous avez enregistrées lors de la tâche précédente (remarque : les valeurs doivent être entre guillemets) :

   a. **AZURE-AI-SEARCH-ENDPOINT** correspond au **point de terminaison** de la tâche précédente.

   b. **index_name** correspond au **nom de l’index** de l’étape 11 de la tâche 2 précédente.

   c. **key** correspond à la **clé de ressource Recherche Azure** de la tâche précédente.

7. Accédez au  **src/app/app.js file** et ajoutez la variable suivante à l’intérieur d’ **OpenAIModel** juste après la ligne azureEndpoint: config.azureOpenAIEndpoint : 

    a. azureApiVersion : '2024-02-15-preview',
   
8. **Ficher** > **Enregistrer sous**.
    
9. Appuyez sur **Ctrl+Maj+d** sur votre clavier, une liste déroulante en haut à gauche s’affiche avec un bouton de lecture vert et le mot Debug > Select the dropdown> sélectionnez **Debug in Test Tool** > appuyez sur **F5**.
10. L’agent de moteur personnalisé s’exécute dans l’outil de débogage que vous avez choisi, qui s’ouvre dans votre navigateur. Vous pouvez poser au bot toutes les questions relatives aux données RAG chargées à l’étape 12 de la tâche 2.
11. Revenez à la fenêtre VS Code de votre application. Sélectionnez la liste déroulante du bouton **Debug** , puis sélectionnez **Debug in Teams (Edge),** puis appuyez sur **F5** ou sur le bouton de lecture vert.
13. Cela ouvrira une nouvelle fenêtre dans votre navigateur Edge. Vous êtes invité à vous connecter. Utilisez les informations de connexion fournies pour vous connecter. Une fois la connexion réussie, fermez la fenêtre.
14. Répétez l’étape 11. Il doit y avoir une fenêtre avec le titre de votre application nouvellement créée. Sélectionnez **Ajouter** > **Ouvrir**.
15. Félicitations ! Vous pouvez maintenant poser à l’agent toute question relatives aux fichiers de données RAG.
16. **Remarque :** cet agent ayant été conçu à des fins éducatives à l’aide de votre propre abonnement, les utilisateurs doivent le supprimer après l’achèvement de ce labo. Pour supprimer un agent personnalisé dans Microsoft Teams, vous pouvez effectuer les opérations suivantes :
- Sélectionnez l’agent que vous souhaitez supprimer, puis cliquez sur l’icône **Plus d’options (…)** et sélectionnez **Supprimer**.
- Supprimez l’agent d’une conversation en sélectionnant les points de suspension dans le fil de discussion et en choisissant **Gérer les applications**.
- Dans l’expérience de création d’un agent, sélectionnez les **points de suspension (...)** et choisissez **Supprimer**.

**FIN DU LABO**
