---
layout: post
title: "Migrer d'&#201;clipse &#224; Intellij"
date: 2013-06-12 11:11
comments: true
categories: [Intellij]
---

Intellij est un IDE Java développé par JetBrains, disponible en deux versions; une version open source **Community Edition** limitée; une version complète **Ultimate** nécessitant l'achat d'une license ([matrice de comparaison](http://www.jetbrains.com/idea/features/editions_comparison_matrix.html)).

Après 8 ans sous d'Eclipse, j'ai décidé de migrer mes projets dessus pour voir si sa réputation était justifiée. 

<img class="middle" src="{{ root_url }}/images/posts/intellij-logo.png" title="logo" >

<!--more-->

# Les points +
Le développement sous Intellij m'a paru bien plus agréable qu'avec Eclipse pour les raisons suivantes :

* Complétion immédiate (il n'est plus nécessaire de faire CTRL+SPACE) et plus intelligente (complétion SQL active même dans un fichier .java)
* Prise en charge native de MAVEN, SVN et GIT (aucun plugin à télécharger)
* Support de nombreux frameworks Play, Grails, Scala... (sous Eclipse 4.2 le plugin scala est en béta et Spring Tool Suite est basé sur Eclipse 3.8)
* Outil de test de services REST inclu (j'en ai profité pour désinstaller HttpRequester sous Firefox)
* Sauvegarde automatique des fichiers (l'historique local du fichier ne dépend pas d'un CTRL+S)
* Partage simple de la configuration de l'IDE, soit par un serveur dédié [JetBrain](http://www.jetbrains.com/idea/features/settings_sync.html), soit avec son [gestionnaire de source](http://devnet.jetbrains.com/docs/DOC-1186)
* Editeur SQL avec complétion et export des resultats (Eclipse le propose également)
* IHM moderne et qui ne gèle pas (le thème Darcula est magnifique)
* Couverture de code intégrée (mais je garde une préférence pour EclEmma dans Eclipse)
* Presse papier avec historique (CTRL+SHIFT+V)
* Zoom+/- avec la molette de la souris (à activer)
* Refactoring plus intelligent (ex : Quand on renomme une classe, les requêtes JPA sont mises à jour)

# Les points -
Si Intellij m'a fait bonne impression, certains fonctionnements par défaut m'ont pertubé dès l'ouverture du premier projet.

### > Le prix
Commençons par le point qui fâche. 
L'acquisition IntelliJ coûtera, la premère fois, 179 € HT pour une licence personnelle (89 € HT pour les étudiants) . 
Les mises à jours sont ensuite 40% moins chères en moyenne. 
A noter également que [des offres](http://blog.jetbrains.com/blog/2013/04/15/50-off-jetbrains-tools-and-help-to-plant-a-billion-trees/) ont existé dans le passé allant jusqu'à 50% de réduction sur le prix des licences.
Pour clore le sujet, la version **Ultimate** est disponible gratuitement 30 jours.

### > Le position du curseur dans l'éditeur
Le curseur dans l'éditeur se positionne là où le pointeur de la souris se trouve, qu'il y ait un retour à ligne ou non dans le fichier source.
Pour retrouver un comportement habituel : *File > Settings > Editor >* et décocher **Allow placement of caret after end of line**.

### > Les raccourcis clavier
La principale difficulté que j'ai rencontrée concerne les raccourcis clavier. 
D'une manière générale, je ne les trouve pas très bien pensés. 
Les combinaisons de touches avec F1...12 ne sont pas pratiques et trop souvent les deux mains sont sollicités.

Mais il est possible de les remplacer par ceux d'Eclipse ou NetBeans. 
Pour cela : *File > Settings > Keymap*

<img class="middle" src="{{ root_url }}/images/posts/intellij_shortcut.png" title="curseur" />

<p class="warning"> CTRL+Y (redo) n'est pas l'inverse de CTRL+Z (undo) mais supprime la ligne sur laquelle est positionné votre curseur. </p>

### > Debug : Popup au survole des variables
Le delai d'affichage de la popup sur les variables en mode Debug est par défaut de 700ms. Pour le changer : *File > Settings > Debugger > Data Views*
et modifier la valeur de **Value tooltips delay(ms)**. En mettant 100ms, la popup s'affiche immédiatement.

# Ressources
JetBrains met à disposition une [FAQ](http://www.jetbrains.com/idea/documentation/migration_faq.html) pour aider la migration d'Eclipse vers Intellij.
On trouve également sur leur site [une liste de raccourcis](http://www.jetbrains.com/resharper/webhelp/Reference__Keyboard_Shortcuts.html) ordonnées par catégorie (Navigation and search, Refactorings...) qui peut être utile d'avoir sous la main.
Enfin, lors du Devoxx 2013, un talk a été consacré aux astuces pour gagner en productivité sur Netbeans, Eclipse et Intellij. 
Je vous invite à suivre la présentation disponible sur [Parleys.com](http://www.devoxx.com/display/FR13/IDE+Java+++astuces+de+productivite+pour+le+quotidien).

# Conclusion
Cette expèrience m'a fait prendre conscience de toutes les lacunes d'Eclipse. 
En effet, il n'est pas normal d'avoir une option pour redémarrer l'IDE, de faire *F5* et *clean* sur un projet pour qu'il s'importe correctement, ou encore de forcer la mise à jour des dépendances Maven après avoir modifié le ```pom.xml```. 
Les developpeurs ont besoin d'un outil fiable qui prend en charge les dernières technologies. 
C'est ce que Intellij propose. Malheureusement, cela a un prix. 
Une chose est sûre, les équipes d'Eclipse doivent se ressaisir. 
Le désamour est croissant depuis la branche 4.x. [Spring Tool Suite](http://www.springsource.org/downloads/sts-ggts) reste basé sur la version 3.8 réputée plus fiable et l'annonce d'[AndroidStudio](http://developer.android.com/sdk/installing/studio.html) basé sur Intellij au dernier Google I/O sont autant de signes qui vont dans ce sens.
C'est finalement Netbeans qui risque de gagner le plus en popularité : à la fois gratuit, plus réactif qu'Eclipse dans les mises à jours et plus stable.