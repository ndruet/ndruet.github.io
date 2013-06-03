---
layout: post
title: "Octopress"
date: 2013-05-27 16:47
comments: true
categories: [Octopress]
---

Mes premiers mots seront consacrés à [Octopress](http://octopress.org), un générateur de blog statique écrit en ruby basé sur [JeKyll](http://jekyllrb.com).

<img class="middle" src="{{ root_url }}/images/posts/octopress-logo.png" title="logo" >

<!--more-->

# Simple
Le site généré avec ne nécessite ni base de données à administrer, ni serveur d'application, seulement un serveur HTTP. 
En quelques lignes de commande ```rake generate|watch|preview|deploy```, on peut ajouter un post et publier sur GitHub. Par défaut les 
articles suivent la synthaxe [Markdown](http://daringfireball.net/projects/markdown/) qui rendra plus simple la migration vers une nouvelle 
plateforme le jour ou Octopress ne sera plus à la mode.

# Thèmes
Les thèmes sont gratuits et assurent le minimum :

* Présentation claire
* Navigation simple 
* Responsive design
* Code HTML5 modifiable

Vous en trouverez sur [http://octopressthemes.com](http://octopressthemes.com/) et d'autres sur [http://www.evolument.com](http://www.evolument.com/blog/2013/03/02/top-10-plus-octopress-themes/)

# Plugins
Octopress gère automatiquement les comptes twitter, google plus, google analytics... simplement en renseignement nos identifiants.
On peut également inclure des Gists dans les posts, des video HTML5 et bénéficier de la coloration syntaxique sans beaucoup d'effort.

# Ressources
Internet regorge de tutos pour débuter ([http://techilm.com](http://techilm.com/blog/2012/07/16/creer-un-blog-sous-octopress-partie-1-presentation/)) mais rien en vaut la documentation officielle d'Octopress et de Jekyll.

# Warning
Le plus compliqué est d'installer Ruby, Octopress (sur Windows dans mon cas) et de personnaliser son thème. 
Les fichiers sont par défaut en ANSI. Au passage des posts en UTF-8 j'ai du m'assurer qu'ils étaient encoder sans [Byte order mark](Byte order mark).
