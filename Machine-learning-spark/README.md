Le problème de prédiction de l'attrition des employés consiste à prévoir si un employé va quitter son emploi ou non. Cela peut être utile pour les entreprises afin de prendre des mesures préventives pour retenir leurs employés précieux et réduire le taux d'attrition.

En utilisant l'ensemble de données https://raw.githubusercontent.com/msellamiTN/Machine-Learning-with-Python/master/data/HR-Employee-Attrition.csv, ce projet vise à construire un modèle prédictif SUPERVISÉ pour résoudre ce problème.

Prérequis
diff

- Docker
- Docker Compose


Explication
Étape 1 : Construction du modèle
Le notebook contenant le code de construction du modèle, exporté de Databricks, est disponible dans les fichiers.

Nettoyage et préparation des données :
La première étape consistait à effectuer une exploration approfondie des données sur l'ensemble de données. Nous avons veillé à ce que les colonnes de l'ensemble de données aient le bon format, vérifié la présence de valeurs NaN et compris les colonnes qui contenaient un nombre important de zéros. En conséquence, nous n'avons trouvé aucune valeur NaN, et les colonnes suivantes avaient des valeurs zéro :
NumCompaniesWorked : 13,4 %, StockOptionLevel : 42,93 %, YearsInCurrentRole : 16,6 %, YearsSinceLastPromotion : 39,52 %, YearsWithCurrManager : 17,89 %. Nous avons déduit que ces valeurs zéro étaient cohérentes avec la signification de zéro dans chaque colonne.
Nous avons également effectué une analyse de corrélation entre différentes colonnes et identifié une forte corrélation entre les colonnes JobLevel et MonthlyIncome. Par conséquent, nous avons décidé de choisir l'une d'elles pour notre analyse, éliminant ainsi la nécessité de travailler avec les deux colonnes.

Construction du pipeline et entraînement et évaluation du modèle :
Pour préparer nos données à l'entraînement, nous avons développé un pipeline qui permet la création et la transformation des caractéristiques. Le pipeline est composé de plusieurs étapes qui sont exécutées en séquence, les données circulant d'une extrémité à l'autre.

Les étapes de notre pipeline sont :

Transformation des caractéristiques :

Convertir les données catégorielles en données codées à l'aide de l'indexation de chaînes et du OneHotEncoder
Mettre à l'échelle chaque variable à une variance unitaire à l'aide du Standar Scaler.
Extraction des caractéristiques :

Convertir nos colonnes régulières en vecteurs de caractéristiques Spark à l'aide de la vectorisation.



Pour entraîner notre modèle, nous avons divisé nos données en deux ensembles : un ensemble d'entraînement contenant 80% des données et un ensemble de test contenant les 20% restants. Nous avons suivi la règle de Pareto pour déterminer la répartition.

Comme notre cas d'utilisation est une classification binaire, nous avons testé deux modèles d'apprentissage automatique : la régression logistique et la forêt aléatoire. Nous avons évalué les performances de ces modèles sur l'ensemble de test en utilisant des mesures standard telles que la précision, le rappel, le score F1 et l'AUC.

