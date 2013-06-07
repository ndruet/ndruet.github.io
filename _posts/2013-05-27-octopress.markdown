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
L’avantage d’un générateur de blog statique est sa simplicité de fonctionnement. Aucune base de données, ni de serveur d’application ne sont nécessaires. 
Quelques lignes de commandes suffisent pour créer un post et le publier sur GitHub. Par défaut les articles suivent la synthaxe 
[Markdown](http://daringfireball.net/projects/markdown/).

Les principales commandes sont :

```
rake generate   # Genère entièrement le site à partir du fichier _config.xml et les répertoires /sources et /saas
rake preview    # Scrute seulement /sources (les fichiers web et les posts) pour les changements, et monte un serveur http://localhost:4000
rake new_post["title"] # Création d'un nouveau post
rake deploy     # Déploiement sur GitHub
```

# Thèmes
Les thèmes sont gratuits, disponibles sur GitHub, s’installent facilement et assurent le minimum :

* Présentation claire
* Navigation simple 
* Responsive design
* Code HTML5 modifiable

Vous en trouverez sur [http://octopressthemes.com](http://octopressthemes.com/) et d'autres sur [http://www.evolument.com](http://www.evolument.com/blog/2013/03/02/top-10-plus-octopress-themes/).

# Plugins
Octopress gère automatiquement les comptes twitter, google+, google analytics… simplement en renseignement ses identifiants dans le fichier ```_config.xml```.
On peut également inclure des Gists, des videos HTML5 et bénéficier de la coloration syntaxique sans trop d’effort.

# Problèmes rencontrés
Du téléchargement d’Octopress à la publication sur Github, tout n’a pas été si simple.
### > UTF-8
Au passage des posts en UTF-8, j’ai du m’assurer qu’ils étaient encoder sans Byte order mark, sans quoi les accents ne s’affichaient pas dans le navigateur. 
C’est la principale raison pour laquelle j’écris les posts avec Notepad++.
### > Windows

Au moment de déployer sur GitHub, j’ai du corriger un problème lié au message d’erreur suivant :
> *‘hellip’ is not recognized as an internal or external command, operable program or batch file.*

et modifier la variable *branch* du fichier ```Rakefile``` afin que l’expression régulière accepte les urls HTTPS.
[Le blog de David Tellander](http://derantell.github.io/blog/2012/12/02/getting-started-with-octopress-on-windows/) m’a beaucoup aidé. On y retrouve en détails ces modifications.

### > GitHub
J’ai également du forcer Octopress a publier sur la branche master (Organization Pages) de Github en modifiant la variable *branch* de ```Rakefile``` sans quoi le blog était pusher sur *gh-pages* (Project Page).
### > Coloration synthaxique
Le site ne mentionne pas que Python (version 2.7.5) est indispensable pour le bon fonctionnement de la coloration synthaxique. Une fois installé, la langue dans les blocs de code est bien prise en compte.

# Ressources
La documentation officielle décrit étape par étape comment installer, rédiger et publier. Pour les utilisateurs sous Windows 
un tour sur [le blog de David Tellander](http://derantell.github.io/blog/2012/12/02/getting-started-with-octopress-on-windows/) vous évitera de vous arracher les cheveux.

#Conclusion

Pour l’instant, Octopress répond parfaitement à mes besoins. Je reste persuadé que si j’étais sous Linux l’installation se serait passée plus simplement. 
Mais une fois tous les problèmes réglés, la publication d’un billet est un jeu d’enfant. Une communauté semble se développer autour du projet (Jekyll de manière plus générale) 
mais l’activité sur GitHub n’est pas dingue ces derniers temps.