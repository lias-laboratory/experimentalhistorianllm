# Experimental Historian LLM

Ce projet de recherche dans les humanités numériques vise à tester les capacités de différents larges modèles de langage (LLM) dans le domaine des réponses à des questions (*question-answering*) en histoire. Deux objectifs principaux nous intéressent au premier chef, sur le fond comme dans la forme :

* Analyser la qualité et la précision des réponses apportées par les LLM sur différents niveaux de questions en histoire.
* Vérifier s'il est possible d'extraire les données prépondérantes dans les réponses générées pour pouvoir les réutiliser par ailleurs.

Toutes les questions ainsi que les résultats obtenus à partir de notre banc d'essai se trouvent dans le fichier [questions-types.xlsx](questions-types.xlsx)

## Modèles de LLM testés

| Technologie   | Modèle           | Nombre de paramètres | Type d’usage | URL                                                       |
|---------------|------------------|----------------------|--------------|-----------------------------------------------------------|
| ChatGPT       | GPT-4            | 170 000 milliards    | Chat         | <https://platform.openai.com/docs/models/gpt-4>           |
| ChatGPT       | GPT-3.5-turbo    | 175 milliards        | Chat         | <https://platform.openai.com/docs/models/gpt-3-5>         |
| Google Bard   | PaLM 2           | ?                    | Chat         | <https://bard.google.com/>                                |
| TextCortex AI | Sophos-2         | 20 milliards et plus | Chat         | <https://textcortex.com/fr/>                              |
| Guanaco       | Guanaco-33b-GGML | 33 milliards         | Chat         | <https://huggingface.co/TheBloke/guanaco-33B-GGML>        |
| Vicuna        | Vicuna-33b-v1.3  | 33 milliards         | Chat         | <https://huggingface.co/lmsys/vicuna-33b-v1.3>            |
| GPT4All       | L13b-snoozy      | 13 milliards         | Chat         | <https://gpt4all.io>                                      |
| Koala         | 13b-diff-v2      | 13 milliards         | Chat         | <https://bair.berkeley.edu/blog/2023/04/03/koala/>        |
| Vigogne       | Instruct-13b     | 13 milliards         | Instruct     | <https://huggingface.co/bofenghuang/vigogne-instruct-13b> |
| Falcon        | Instruct-7B      | 7 milliards          | Instruct     | <https://huggingface.co/tiiuae/falcon-7b-instruct>        |

## Requêtes testées

Un ensemble de 62 questions à propos de l'histoire de l'ancien Poitou (actuellement situé dans la région Nouvelle-Aquitaine) a été créé pour servir de base dans notre étude. Nous avons décomposé cet ensemble en sous-classes de questions afin de vérifier les aptitudes des LLM à répondre avec une même précision en fonction du type de questions auxquels ils sont confrontés.

| Types de questions  | Type de données attendu dans les réponses  | Nombre de questions |
|---------------------|--------------------------------------------|---------------------|
| Quantitatif (fermé) | Donnée numérique                           |          16         |
| Qualitatif (fermé)  | Métadonnée                                 |          15         |
| Qualitatif (fermé)  | Liste de données                           |          10         |
| Qualitatif (ouvert) | Définition/Description                     |          16         |
| Qualitatif (ouvert) | Description détaillée d'une problématique  |          5          |

Ces questions ont été réparties dans 5 thématiques aux caractéristiques diverses :

* Bataille de Poitiers (732)
* Bataille de Poitiers (1356)
* 3ème guerre de religion (1568-1570)
* Siège de La Rochelle (1627-1628)
* Artisanat (époque moderne)

Ces cinq sujets représentent des faits historiques tantôt très traités sur le Web mais plein de zones d'ombre pour les historiens (la bataille de Poitiers en 732 par exemple), tantôt bien connus des spécialistes (la troisième guerre de religion par exemple), ou encore relativement équivoque et complexe (l'artisanat à l'époque moderne). Nous avons cherché également à créer de potentielles confusions thématiques, ce qui explique la présence de sujets ayant été multiples dans l'histoire de France (plusieurs batailles de Poitiers ou sièges de La Rochelle notamment).

## Méthodologie

Nous ne nous sommes pas contentés de poser nos questions brutes aux différents LLM testés, nous avons souhaité affiner l'analyse en proposant des variantes et vérifier si les LLM ont la capacité de bien répondre quand bien même la forme de la requête varie. Dans un premier temps, nous avons créé pour chaque question une autre variante dont le sens général est équivalent (par exemple : "Quand a eu lieu précisément la bataille de Poitiers avec Jean le Bon ?" est la question originale, et "Quelle est la date exacte de la bataille de Poitiers avec Jean le Bon ?" est sa variante). Ensuite, chacune de ces variantes a été dupliquée pour obtenir les mêmes questions en requêtes de mots clés, afin de vérifier si les LLM s'adaptent mieux à des requêtes en langue naturelle ou de mots clés (ainsi, nos requêtes d'exemples deviennent respectivement "période précise de la bataille de Poitiers avec Jean le Bon" et "date exacte de la bataille de Poitiers avec Jean le Bon"). Par conséquent, chaque question génère en réalité quatre requêtes à tester, et cela nous permet à la fois d'analyser si les LLM réagissent différemment selon le type de requête, mais aussi s'ils sont capables de fournir une bonne réponse dans chaque cas. Par ailleurs, pour compléter ce processus et s'assurer que les LLM ne répondent pas correctement uniquement par chance ou par hasard, nous avons demandé une régénération pour chaque requête posée. En définitive, nous obtenons huit réponses par question, pour chaque LLM.

Comme nous souhaitions également tester les variantes sémantiques et la diachronie, nous avons créé pour certains questions qualitatives fermées des variantes complémentaires en utilisant le nom des entités nommées de la période ciblée (pour répondre notre exemple, nous avons proposé les variantes "Quelle est la date exacte de la bataille de Poictiers avec Jehan le Bon ?" et "date exacte bataille de Poictiers avec Jehan le Bon"). Nous objectif était de vérifier si les LLM ont la capacité de faire des analogies entre les entités nommées actuelles et celles du passé, tout en répondant correctement à la question posée. Au total, ce sont donc 5360 réponses qui ont été vérifiées à partir de nos 5 thématiques et 62 questions d'origine.

## Résultats obtenus

Nous avons comparé la précision des réponses (nombre de bonnes réponses sur le total des requêtes analysées) par LLM et nous avons obtenu ces résultats : 

|                  |             Résultats             |         |             Précision             |
|                  |-----------------|-----------------|         |-----------------|-----------------|
|                  | Bonnes réponses | Autres réponses |         | Bonnes réponses | Autres réponses |
|------------------|-----------------|-----------------|---------|-----------------|-----------------|
| ChatGPT (GPT4)   |       291       |       245       |         |      54,29%     |     45,71%      |
| ChatGPT (GPT3.5) |       276       |       260       |         |      51,49%     |     48,51%      |
| Bard             |       246       |       290       |         |      45,90%     |     54,10%      |
| TextCortex       |       277       |       259       |         |      51,68%     |     48,32%      |
| Guacano          |       183       |       353       |         |      34,14%     |     65,86%      |
| Vicuna           |       197       |       339       |         |      36,75%     |     63,25%      |
| GPT4All          |       95        |       441       |         |      17,72%     |     82,28%      |
| Koala            |       120       |       416       |         |      22,39%     |     77,61%      |
| Vigogne          |       94        |       442       |         |      17,54%     |     82,46%      |
| Falcon           |       22        |       514       |         |       4,10%     |     95,90%      |
|------------------|-----------------|-----------------|---------|-----------------|-----------------|
| Totaux           |      1801       |       3559      | Moyenne |      33,60%     |     66,40%      |

Nous avons également dressé un tableau des résultats par thématique historique, afin de vérifier les différences de précision des LLM testés :

| Thématiques                              | Bonnes réponses | Autres réponses | Précision |
|------------------------------------------|-----------------|-----------------|-----------|
| Bataille de Poitiers (732)               |       376       |       664       |  36,15 %  |
| Bataille de Poitiers (1356)              |       425       |       615       |  40,87 %  |
| Troisième guerre de religion (1568-1570) |       395       |       645       |  37,98 %  |
| Siège de La Rochelle (1627-1628)         |       387       |       653       |  37,21 %  |
| Artisanat à l’époque moderne             |       218       |       982       |  18,17 %  |

## Licence

Détails du contrat de licence de l'expérience : [LICENCE](LICENSE)

## Contributeurs

* [Mathieu CHARTIER](https://criham.labo.univ-poitiers.fr/membres/mathieu-chartier/) (CRIHAM, Université de Poitiers)
* [Stéphane JEAN](https://www.lias-lab.fr/members/stephanejean/) (LIAS, ISAE-ENSMA et université de Poitiers)
* [Guillaume BOURGEOIS](https://criham.labo.univ-poitiers.fr/membres/guillaume-bourgeois/) (CRIHAM, Université de Poitiers)
* Nabil DAKKOUNE (LIAS, ISAE-ENSMA et université de Poitiers)
