---
layout: post
title: "D'&#201;clipse &#224; Intellij"
date: 2013-06-12 11:11
comments: true
categories: [Intellij]
---

Intellij est un IDE Java développé par JetBrains, disponibles en deux versions; une version open source **Community Edition** limité; une version complète **Ultimate** qui nécessite l'achat d'une license.

Après 8 ans sous d'Eclipse, j'ai décidé de migrer mes projets dessus pour voir si sa réputation était justifiée. 

<img class="middle" src="{{ root_url }}/images/posts/intellij-logo.png" title="logo" >

<!--more-->

# Les points +
Le développement sous Intellij est bien plus agréable qu'avec Eclipse pour les raisons suivantes :

* Complétion immédiate (il n'est plus nécessaire de faire CTRL+SPACE)
* Prise en charge native de MAVEN, SVN et GIT (aucun plugin à télécharger)
* Support de nombreux frameworks Play, Grails, Scala... (sous Eclipse 4.2 le plugin scala est en béta et Spring Tool Suite est basé sur Eclipse 3.8)
* Outil de test de service REST inclu (j'en ai profité pour désinstaller HttpRequester sous Firefox)
* Sauvegarde automatique des fichiers (l'historique local du fichier ne dépend pas d'un CTRL+S)
* Partage de la configuration de l'IDE simple (soit par un serveur dédié [JetBrain](http://www.jetbrains.com/idea/features/settings_sync.html), soit avec son [gestionnaire de source](http://devnet.jetbrains.com/docs/DOC-1186)
* Complétion dans l'éditeur SQL
* IHM moderne qui ne gèle pas (le thème Darcula est magnifique)
* Couverture de code intégrée
* Presse papier avec historique (CTRL+SHIFT+V)
* Zoom+/- avec la molette de la souris (à activer)

# Les points -
Si Intellij m'a fait bonne impression. Certains fonctionnement par défaut m'ont géné dès l'ouverture 
du premier projet.

### > Le position du curseur dans l'éditeur
Le curseur dans l'éditeur se positionne là ou le pointeur de la souris se trouve, qu'il y ait un retour à ligne ou non.
Pour retrouver un comportement habituel : *File > Settings > Editor >* et décocher **Allow placement of caret after end of line**.

### > Les raccourcis clavier
S'adapter aux nouveaux raccourcis est le principale challenge. Si j'ai fais l'effort
de les apprendre, il est possible de les remplacer par ceux d'Eclipse ou NetBeans. Pour cela : *File > Settings > Keymap*

<img class="middle" src="{{ root_url }}/images/posts/intellij_shortcut.png" title="curseur" >

### > Debug : Popup au survole des variables
Le delais d'affichage de la popup sur les variables en mode Debug est par défaut de 500ms. Pour modifier ce délais : *File > Settings > Debugger > Data Views*
et modifier la valeur de **Value tooltips delay(ms)**. En mettant 100ms, la popup s'affiche immédiatement.

# Conclusion
Cette aventure m'a fait prendre conscience de toutes les lacunes d'Eclipse. En effet, il n'est pas normal d'avoir une option pour redémarrer l'IDE, de devoir faire *F5* et *clean* sur un projet pour qu'il s'importe correctement,
ou encore de forcer la mise à jour des dépendances Maven après avoir modifié le ```pom.xml```. 
Les developpeurs ont besoin d'un outil fiable qui prend en charge les dernières technologies. C'est ce que Intellij propose. Malheureusement, cela a un prix. 
Mais il est certain que les équipes d'Eclipse doivent se ressaisir. Le désamour est croissant depuis la branche 4.x. 
[Spring Tool Suite](http://www.springsource.org/downloads/sts-ggts) reste basé sur la version 3.8 réputée plus fiable et l'annonce d'[AndroidStudio](http://developer.android.com/sdk/installing/studio.html) basé sur Intellij au dernier Google I/O sont autant de signes qui vont dans ce sens.

JetBrains met à disposition une [FAQ](http://www.jetbrains.com/idea/documentation/migration_faq.html) pour aider la migration.