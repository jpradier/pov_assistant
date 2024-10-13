## Approche scriptée mais adaptée grâce à l'IA Générative (LLM-powered)

Nous aimerions revenir sur l'approche **scripté** de watsonx Assistant: 
Le script ou Action est une séquence simple d'étape de collecte de l'information suivi d'une action (ouverture d'un ticket, activation d'une option ou transfert vers un opérateur).
Le script offre plusieurs avantages dont:

- simplicité de construction du script pour un agilité maximale
- maîrise totale des formulations pour prévenir tout risque.

Le LLM (Granite) intégré et sans coût additionnel permet toutefois de s'adapter aux différentes énonciations du client (voir vidéo ci-contre), il agit comme un super NLU pour faciliter la collecte d'information.

https://github.com/user-attachments/assets/05abebe8-e711-4ba3-afe2-579ce60c871a

Cette collecte utilisant un <i>petit</i> LLM intégré et avec une faible latence permet aussi d'adapter le script en évitant de poser les questions correspondantes aux informations déjà collectées. 

Les formulations restent cependant _en dur_. Aussi dans l'exemple, "Mon nom est **Francois**, mais c'est ma femme **Kim** qui est titulaire de la ligne",
l'outil va bien reconnaitre que la réponse à la question: "Pouvez-vous me confirmer le nom du titulaire de la ligne ?" est **Kim**. 
Mais la formulation suivante est _en dur_: "Merci beaucoup, **Kim** ...". Elle est en effet variabilisée et non générée. Dans ce cas, elle est erronée.
Pour bien nommer le locuteur, il faudrait introduire une nouvelle variable nom_du_locuteur en plus du nom_du_titulaire.
On peut aussi rester dans la simplicité et ne pas nommer le locuteur.

## Recours aux LLMs pour mener la conversation (LLM-driven)

Dans certains scénario, il n'est pas possible de simplifier et le recours à une formulation générée est le meilleure choix.
Ainsi dans le scénario MétéoDuRéseau, l'obtention de l'adresse est complexe avec la formulation qui dépend de plusieurs choix:
incident au domicile du titulaire de la ligne, incident dans une rue sans ville identifiée, ou à l'inverse dans une ville mais dans une rue trop longue, ou bien au pied d'un monument iconique.
Utiliser des variables et d'étapes rendent le script trop complexe. Un LLM peut parfaitement répondre à cette problèmatique et être configuré avec un prompt de qq lignes.

Les LLMs de dernière génération disponible sur **watsonx** tel que Llama 3.2 ou Mistral Large 2407 peuvent même aller au delà et orchester l'appel à des fonctions ou API et donc prendre en charge l'intégralité du scénario. Voir vidéo ci-contre.

https://github.com/user-attachments/assets/a3aeeda1-ab78-49f3-bdd2-e0c183e6f18a

Les LLMs, s'ils répondent parfaitement à ces cas d'usage, ont qq chalenges:

- le prix d'inference. Dans ce cas d'usage (formulation générée), le prix d'inférence n'est pas inclus dans le prix d'usage de watsonx Assistant.
Le prix d'inférence sur [watsonx](https://dataplatform.cloud.ibm.com/docs/content/wsj/getting-started/wxai-runtime-plans-genai.html?context=wx#billing-classes-by-multiplier) sont fonction du nombre de tokens mais aussi de la taille du modèle. Un prix d'inférence de 60 centimes pour le million de tokens permet néanmoins leur utilisation dans un service grand public à condition de ne pas utiliser les modèles les plus sophistiqués avec raisonnement et function calling.

- la latence. Une latence trop importante n'est pas compatible avec un usage grand public, en particulier avec le canal téléphonique.
Là encore, il faut priviliégié les modèles plus petit.

- leur vulnérabilité. Comme le montre la vidéo ci-contre, un LLM peut s'avérer problématique et exposer plusieurs risques (comme la fuite de données personnelles). IBM a repertorié ces risques dans un [atlas de risques](https://dataplatform.cloud.ibm.com/docs/content/wsj/ai-risk-atlas/ai-risk-atlas.html?context=wx&locale=fr).

https://github.com/user-attachments/assets/a50fee27-1217-4179-bcd7-4c918bde987f

IBM watsonx offrent un certain nombre d'outils dans son module de gouvernance pour maîtriser ces risques (garde fous ou guard rails , ainsi que supervision active des LLMs) et vous permettrent de mitiger les risques réputationnels, opérationnels ou réglementaires associés à l'utilisation des LLMs pour le grand public

## Panacher script et IA Générative.

Vous l'aurez compris avec watsonx Assistant et son extension watsonx Orchestrate, vous pourrez panacher l'utilisation de script avec l'utilisation des LLMs ou même de règles de décisions.
Vous aurez la possibilité d'arbitrer en fonction des scénarios, la méthode la plus adaptée au ROI, aux exigences de flexibilité et de maîtrise et cela en fonction de l'exposition aux risques.

![Different Type of Actions](https://github.com/user-attachments/assets/8cec4696-6852-43bd-90f2-01566ff54aae)


