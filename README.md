# Experimental Historian LLM

This research project in digital humanities aims to evaluate the capabilities of various large language models (LLMs) in the domain of question-answering in history. Two primary objectives are of particular interest, both in substance and in form:
* to analyze the quality, the accuracy and the reliability of responses provided by LLMs across different levels of historical questions,
* to assess the feasibility of extracting predominant data from generated responses for potential reuse elsewhere.

All questions along with the results obtained from our testbed are documented in the file [questions-and-data.xlsx](questions-and-data.xlsx)

## LLM models tested

| Technology | Specific feature | Model used      | Parameters | Type of use | Release date |
|------------|------------------|-----------------|------------|-------------|--------------|
| ChatGPT    | Multimodal       | GPT-4           | 170,000 bn | Chat        | 03/2023      |
| Bard       | Multimodal       | PaLM 2          | ?          | Chat        | 03/2023      |
| Copilot    | Multimodal       | Prometheus      | ?          | Chat        | 09/2023      |
| Gemini     | Multimodal       | Gemini-1.0      | ?          | Chat        | 12/2023      |
| Mistral AI | FR/Mixtral       | Mixtral-8x7b    | 12/45 bn   | Instruct    | 12/2023      |
| Vigogne    | FR/Mistral       | Vigostral-7b    | 7 bn       | Instruct    | 10/2023      |
| Vigogne    | FR/Llama         | Instruct-13b    | 13 bn      | Instruct    | 03/2023      |
| Guanaco    | Llama            | Guanaco-33b     | 33 bn      | Chat        | 05/2023      |
| Vicuna     | Llama            | Vicuna-33b-v1.3 | 33 bn      | Chat        | 03/2023      |
| Koala      | Llama            | 13b-diff-v2     | 13 bn      | Chat        | 04/2023      |
| ChatGPT    |                  | GPT-3.5-Turbo   | 175 bn     | Chat        | 03/2022      |
| TextCortex |                  | Sophos-2        | 20 bn      | Chat        | ?            |
| GPT4All    |                  | L13b-snoozy     | 13 bn      | Chat        | 03/2023      |
| Falcon     |                  | Instruct-7B     | 7 bn       | Instruct    | 04/2023      |

## Queries tested

A set of 62 questions regarding the history of ancient Poitou in France (currently located in the Nouvelle-Aquitaine region) was created to serve as a foundation for our study. We decomposed this set into subclasses of questions to assess the abilities of LLMs to respond with consistent accuracy based on the type of questions they encounter.

| Types of questions  | Data type expected in responses   | Number of questions |
|---------------------|-----------------------------------|---------------------|
| Quantitatif (fermé) | Numeric data                      |          16         |
| Qualitatif (fermé)  | Metadata                          |          15         |
| Qualitatif (fermé)  | Data list                         |          10         |
| Qualitatif (ouvert) | Definition/Description            |          16         |
| Qualitatif (ouvert) | Detailed description of a problem |          5          |

These questions were divided into 5 themes with various characteristics:

* Bataille de Poitiers (732)
* Bataille de Poitiers (1356)
* 3ème guerre de religion (1568-1570)
* Siège de La Rochelle (1627-1628)
* Artisanat (époque moderne)

These five topics encompass historical facts that are sometimes extensively covered on the web yet contain many gaps for historians (such as the Battle of Poitiers in 732), sometimes well-known to specialists (such as the Third War of Religion), or even relatively ambiguous and complex (such as craftsmanship in the modern era). We also aimed to create potential thematic confusions, which accounts for the inclusion of subjects that have occurred multiple times in French history (several battles of Poitiers or sieges of La Rochelle, for example).

## Méthodology

We didn't merely pose our raw questions to the various tested LLMs; we aimed to refine the analysis by offering variants to verify if LLMs can provide accurate responses even when the query form varies. Initially, for each question, we created another variant with an equivalent general meaning (for example: "When did the battle of Poitiers with Jean le Bon precisely occur?" is the original question, and "What is the exact date of the battle of Poitiers with Jean le Bon?" is its variant ***). Subsequently, each of these variants was duplicated to obtain the same questions as keyword queries, to verify if LLMs adapt better to natural language or keyword queries (thus, our example queries become respectively "precise period of the battle of Poitiers with Jean le Bon" and "exact date of the battle of Poitiers with Jean le Bon"). Consequently, each question actually generates four queries to be tested, allowing us to analyze if LLMs react differently according to the query type, and also if they are capable of providing a correct response in each case. Furthermore, to complete this process and ensure that LLMs do not respond correctly only by chance, we requested regeneration for each posed query. Ultimately, we obtain eight responses per question, for each LLM.

As we also aimed to test semantic variations and diachrony, we created complementary variants for certain closed qualitative questions using named entity names from the targeted period (to address our example, we proposed variants such as "What is the exact date of the battle of Poictiers with Jehan le Bon?" and "exact date battle of Poictiers with Jehan le Bon"). Our objective was to verify if LLMs have the capability to draw analogies between current named entities and those from the past, while still correctly answering the posed question. In total, 7504 responses were thus verified based on our 5 themes and 62 original questions (268 queries).

*** All questions were asked in French in our study, we present them in English here only for ease of understanding.

## Results

We compared the accuracy of responses (number of correct answers out of the total queries analyzed) by LLM, and we obtained these results:

|&nbsp;|Résults<br/>*Correct answers*|Results<br/>*Other answers* |&nbsp;|Precision<br/>*Correct answers*|
|-------------------------|:---------------:|:---------------:|:-------:|:---------------:|
| Gemini                  |       377       |       159       |&nbsp;   |      70.34%     |
| Copilot                 |       303       |       233       |&nbsp;   |      56.53%     |
| ChatGPT (GPT-4)         |       287       |       249       |&nbsp;   |      53.54%     |
| ChatGPT (GPT-3.5-Turbo) |       273       |       263       |&nbsp;   |      50.93%     |
| Mixtral-8x7b            |       272       |       264       |&nbsp;   |      50.75%     |
| TextCortex AI           |       266       |       270       |&nbsp;   |      49.63%     |
| Bard                    |       244       |       292       |&nbsp;   |      45.52%     |
| Guanaco                 |       184       |       352       |&nbsp;   |      34.33%     |
| Vicuna                  |       197       |       339       |&nbsp;   |      36.75%     |
| Koala                   |       120       |       416       |&nbsp;   |      22.39%     |
| GPT4All                 |       95        |       441       |&nbsp;   |      17.72%     |
| Vigogne                 |       94        |       442       |&nbsp;   |      17.54%     |
| Vigostral               |       86        |       450       |&nbsp;   |      16.04%     |
| Falcon                  |       22        |       514       |&nbsp;   |      4.10%      |
| **Totals**              |    **2820**     |     **4684**    | **Average**|      37.58%      |

We also compiled a histogram of results by historical theme to verify the differences in precision and in reliabily among the tested LLMs:

![Reliability and precision rate by historical theme](images/Figure-1.jpg?raw=true "Reliability and precision rate by historical theme")

## Licence

License Agreement Details: [LICENCE](LICENSE)

## Contributeurs

* [Mathieu CHARTIER](https://criham.labo.univ-poitiers.fr/membres/mathieu-chartier/) (CRIHAM, Université de Poitiers)
* [Stéphane JEAN](https://www.lias-lab.fr/members/stephanejean/) (LIAS, ISAE-ENSMA et université de Poitiers)
* [Guillaume BOURGEOIS](https://criham.labo.univ-poitiers.fr/membres/guillaume-bourgeois/) (CRIHAM, Université de Poitiers)
* Nabil DAKKOUNE (LIAS, ISAE-ENSMA et université de Poitiers)
