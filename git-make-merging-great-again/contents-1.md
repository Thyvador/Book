# Pourquoi les merges peuvent-ils mal se passer point de vue code ?

**Date de rendu finale : March 2018 au plus tard**

Remarques :

Les titres peuvent changer pour etre en adéquation avec votre étude.

De même il est possible de modifier la structure, celle qui est proposée ici est là pour vous aider.

Utilisez des références pour justifier votre argumentaire, vos choix etc.

## Authors

* Chennouf Mohamed &lt;mohamed.chennouf@etu.unice.fr&gt; 
* Huang Shiyang &lt;shiyang.huang@etu.unice.fr
* Swiderska Joanna &lt;joanna.swiderska@etu.unice.fr&gt;
* Wilhelm Andreina &lt;andreina-simonett.wilhelm-garcia@etu.unice.fr&gt;

## I. Research context /Project

_Préciser ici votre contexte._

_Pourquoi c'est intéressant._



Durant nos études et nos expériences professionnelles, nous avons tous déjà été confronté à travailler en équipe sur des projets divers et variés. Dans la majorité des cas, nous utilisons git pour versionner nos travaux. Au sein d’une équipe de travail, il est courant de créer des branches avec git afin que les membres de l’équipe puissent travailler sur des parties du projet sans impacter le projet actuel.

Une fois le travaille sur la branche X est accompli, il est nécessaire d’ajouter ce travail dans la branche principale du projet. Pour synchroniser ces branches, il existe deux méthodes: Merge et Rebase.

Pour notre étude nous nous intéressons aux merges car c’est la synchronisation qu’on utilise le plus souvent durant nos projets. Merge permet d’avancer la branche principale en incorporant le travail d’une autre branche. Cette opération join et fusionne les deux points de départ de ces deux branches dans un commit de fusion. 	

Voici un schéma pour illustrer un merge :

![1. Sch&#xE9;ma d&#x2019;un merge](../.gitbook/assets/image.png)

Dans notre problématique on considère qu’un merge c’est mal passé lorsque le projet ne se compile pas ou s'exécute de façon inattendue \(erreur …\).

Bien que git soit un excellent logiciel de gestion de versions , les merges nous ont parfois causé quelques problèmes. En effet, il nous est déjà arrivé d’avoir des conflits sur des merges ou des merges qui se passent bien mais qui entraînent des erreurs dans le code. 

## II. Observations/General question

1. _Commencez par formuler une question sur quelque chose que vous observez ou constatez ou encore une idée émergente. Attention pour répondre à cette question vous devrez être capable de quantifier vos réponses._
2. _Préciser bien pourquoi cette question est intéressante de votre point de vue et éventuellement en quoi la question est plus générale que le contexte de votre projet \(ex: Choisir une libraire de code est un problème récurrent qui se pose très différemment cependant en fonction des objectifs\)_

_Cette première étape nécessite beaucoup de réflexion pour se définir la bonne question afin de poser les bonnes bases pour la suit._  
	

**1. Pourquoi les merges provoquent des conflits ?**

En nous documentant et en reliant nos sources, nous savons que les conflits de merge se produisent lorsqu'on fusionne des branches ayant des commits concurrents. Git a besoin de notre aide pour décider quelles modifications seront intégrées à la fusion finale. La plupart du temps cela a lieu :

*  lorsque plusieurs utilisateurs modifient la même section de code.
*  lorsqu'une personne modifie un fichier et une autre le supprime.

Nous avons décidé de nous contenter de ces explications pour pouvoir explorer et approfondir la seconde sous-question: _2. Pourquoi les merges se passent bien mais entraînent des erreurs dans le code ?_ Nous estimons que cette sous problématique est très intéressante car les équipes de développeurs sont souvent amenés à changer du code et à impacter les fonctionnalités générales du système.

\*\*\*\*

**2. Pourquoi les merges se passent bien mais entraînent des erreurs dans le code ?**

Nous nous sommes dit qu’il serait possible qu’un merge se passe bien mais qu’il entraîne des erreurs dans le code. Afin de prouver que ce cas existe, nous avons pris les deux exemples suivants comme point appuis :

* Un merge qui se passe bien mais le projet ne se compile pas car il y a une ou plusieurs fautes de codes comme par exemple une erreur de frappes.
* Un merge qui se passe bien et il n’y a pas d’erreur de compilation mais certaines fonctions du projet ne marchent pas car il y a des modifications sur des interfaces ou des conditions qui ont impacté l’intégralité du système.

Ces deux exemples nous amène à nous poser la sous question suivante :

**2.1. Comment repérer qu’un système ne se compile pas ou se compile mais a un comportement inattendu ?**

À nos connaissances, le moyen le plus efficace pour savoir si un projet ne compile pas est de s'intéresser aux outils d'intégration continue qui propose pour la plupart des états du projet lors de chacun merge.

Par exemple, sur les outils Jenkins et Travis, lorsqu’un projet ne compile pas un voyant rouge est affiché alors que lorsque les tests ne passent pas un voyant orange est affiché. Nous avons fait l’hypothèse que le projet compile et ne marche pas lorsque les tests ne passent pas.

De cette manière, en inspectant les outils intégrations, il nous sera possible de déterminer quelles sont les merges qui se sont mal passé. Pour débuter, nous allons choisir un projet qui:

* utilise un langage qu’on connais.
* a un accès public à son outils d'intégration continue.
* a suffisamment de merge qui se passe mal.

**2.2. Comment repérer l’erreur dans le merge ?**

Nous chercherons la cause de l’erreur de la construction du système suite à un merge en inspectant les logs erreurs causé par le “build”. Pour cela nous prévoyons utiliser un outil s’il existe ou de le faire nous même.

## III. Information Gathering

_Préciser vos zones de recherches en fonction de votre projet,_

1. _les articles ou documents utiles à votre projet_
2. _les outils_

**1. Articles**

Nous avons utilisé les articles qui étaient les plus proches à notre sujet pour nous renseigner \_\_\_\_\_\_:

* “SWEBOK, Chap 5 Maintenance”: [https://empear.com/docs/CodeSceneBook.pdf](https://empear.com/docs/CodeSceneBook.pdf)
* "The Impact of Continuous Integration on Other Software Development Practices: A Large-Scale Empirical Study": [ https://cmustrudel.github.io/papers/ase17ci.pdf](%20https://cmustrudel.github.io/papers/ase17ci.pdf)

**2. Outils**

Nous avons créé un logiciel pour inspecter les logs du build de l'outil d'intégration continue. Il extrait automatiquement certaines informations sur les pull requests et le répertoire qui vont nous permettre de répondre à nos questions. Ces informations sont détaillées dans la section suivante.

**2.1. Métriques**

Information extrait pour mesurer la fréquence des conflits de merges dans un répertoire de git:

* Nombre de merges
* Nombre de merges mal passés \(erreurs de compilations / erreurs de tests\)
* Nombre de lignes totales
* Nombre de lignes mergés
* Nombre de contributeurs
* Nombre de branches
* La divergence entre les versions de branche master et les autres branches
* Nombre de tests en erreurs

**2.2. KPI**

* Résultat de CI \(logs … \)
* Marque conflit git 

## IV. Hypothesis & Experiences

1. _Il s'agit ici d'énoncer sous forme d' hypothèses ce que vous allez chercher à démontrer. Vous devez définir vos hypothèses de façon à pouvoir les mesurer facilement. Bien sûr, votre hypothèse devrait être construite de manière à vous aider à répondre à votre question initiale.Explicitez ces différents points._
2. _Test de l’hypothèse par l’expérimentation. 1. Vos tests d’expérimentations permettent de vérifier si vos hypothèses sont vraies ou fausses. 2. Il est possible que vous deviez répéter vos expérimentations pour vous assurer que les premiers résultats ne sont pas seulement un accident._
3. _Explicitez bien les outils utilisés et comment._
4. _Justifiez vos choix_

\_\_

Expliquer les clauses avec de diagrams si c'est possible

## V. Result Analysis and Conclusion

1. _Analyse des résultats & construction d’une conclusion : Une fois votre expérience terminée, vous récupérez vos mesures et vous les analysez pour voir si votre hypothèse tient la route._ 

\_\_![](../.gitbook/assets/logo_uns%20%283%29.png) _UCA : University Côte d'Azur \(french Riviera University\)_

## VI. Tools \(facultatif\)

_Précisez votre utilisation des outils ou les développements \(e.g. scripts\) réalisés pour atteindre vos objectifs. Ce chapitre doit viser à \(1\) pouvoir reproduire vos expériementations, \(2\) partager/expliquer à d'autres l'usage des outils_.



Nous avons développé un script en python où nous utilisons l'API Git pour extraire l'information nécessaire.

## VI. References

1.

1. 
