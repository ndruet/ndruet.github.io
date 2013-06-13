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
L’avantage majeur d’un générateur de blog statique est sa simplicité de fonctionnement. Aucune base de données, ni de serveur d’application ne sont nécessaires. On obtient donc un site qui tient la charge
si son audience grimpe. Quelques lignes de commandes suffisent pour créer un post et le publier sur GitHub. Par défaut les articles suivent la synthaxe 
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
L'interfaçage avec les comptes twitter, google+, google analytics… s'effectue simplement en renseignement ses identifiants dans le fichier ```_config.xml```.
On peut également inclure des Gists, des videos HTML5 et bénéficier de la coloration syntaxique sans trop d’effort.

# Problèmes rencontrés
Du téléchargement d’Octopress à la publication sur Github, tout n’a pas été si simple. Heureusement [Le blog de David Tellander](http://derantell.github.io/blog/2012/12/02/getting-started-with-octopress-on-windows/) m’a été d'un grand secours pour résoudre la majorité des problèmes cités ci-dessous.

### > UTF-8 - Les accents
Les accents m'ont posés deux problèmes :

* La commande rake generate échoue si un accent est présent dans le titre du post, dans la partie descriptive du post [YAML](http://fr.wikipedia.org/wiki/YAML ). Pour contourner cette contrainte, j'ai remplacé les lettres par leur [codes ISO](http://www.commentcamarche.net/contents/489-caracteres-speciaux-html).
* Pour que les accents s'affichent dans le corps du post, j'ai du encoder les posts en UTF-8 (sans [Byte Order Mark](http://en.wikipedia.org/wiki/Byte_order_mark#UTF-8) comme précisé dans [la documentation Jekyll](http://jekyllrb.com/docs/frontmatter/)  ).</br></br>

### > Windows - Commande inexistante
Au moment de déployer sur GitHub, le message suivant s'est affiché :
> *‘hellip’ is not recognized as an internal or external command, operable program or batch file.*

La correction a consisté à remplacer ```&hellip;``` par ```...``` dans le fichier ```RakeFile``` à la ligne suivante :
```
    system "echo 'My Octopress Page is coming soon &hellip' > index.html"
```
### > GitHub - HTTPS et les branches
Le client SSH étant absent de mon post, j'ai du modifié la variable *branch* du fichier ```Rakefile``` pour que l’expression régulière accepte les urls HTTPS au déploiement du blog. 
Mais une fois l'URL acceptée, conséquence directe ou non, Octopress n'a jamais voulu publier sur une autre branche que *gh-pages* (Project Page) au lieu de master (Organization Pages). 
J'ai donc finalement préciser la branche dans le fichier ```Rakefile``` :
```
branch = 'master'
project = ''
```
  
### > Coloration synthaxique
L'indication de la lanque dans les blocs de code cassait la génération du site. En effet [Python en version 2.7.5](http://www.python.org/download/releases/2.7.5/) est indispensable pour l'application de la coloration synthaxique.

# Ressources
La documentation officielle décrit étape par étape comment installer, rédiger et publier. Pour les utilisateurs sous Windows, 
un tour sur [le blog de David Tellander](http://derantell.github.io/blog/2012/12/02/getting-started-with-octopress-on-windows/) vous évitera de vous arracher les cheveux.

#Conclusion

Pour l’instant, Octopress répond parfaitement à mes besoins. Je suis persuadé que si j’étais sous Linux ma première publication se serait passée plus simplement. 
Mais une fois tous les problèmes réglés, la publication d’un billet est un jeu d’enfant. Une communauté semble se développer autour du projet (Jekyll de manière plus générale) 
mais l’activité sur GitHub n’est pas dingue ces derniers temps.