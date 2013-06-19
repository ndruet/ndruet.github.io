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
L’avantage principal d’un générateur de blog statique est sa simplicité de fonctionnement. 
Aucune base de données, ni de serveur d’application ne sont nécessaires. 
On obtient donc un site qui tient la charge même avec une forte audience. 

Octopress permet en quelques lignes de commande de créer un post et publier sur GitHub. 
Les principales commandes sont :

```
rake generate   # Genère entièrement le site à partir du fichier _config.xml et les répertoires /sources et /saas
rake preview    # Scrute seulement /sources (les fichiers web et les posts) pour les changements, et monte un serveur http://localhost:4000
rake new_post["title"] # Création d'un nouveau post
rake deploy     # Déploiement sur GitHub
```
Par défaut les articles suivent la synthaxe [Markdown](http://daringfireball.net/projects/markdown/).

# Thèmes
Les thèmes sont disponibles sur GitHub, s’installent facilement et assurent le minimum :

* Présentation claire
* Navigation simple 
* Responsive design
* Code HTML5 modifiable

Vous en trouverez sur [http://octopressthemes.com](http://octopressthemes.com/) et d'autres sur [http://www.evolument.com](http://www.evolument.com/blog/2013/03/02/top-10-plus-octopress-themes/).

# Plugins
L'interfaçage avec les comptes twitter, google+, google analytics… s'effectue simplement en renseignement ses identifiants dans le fichier ```_config.xml```.
On peut également inclure des Gists, des videos HTML5 et bénéficier de la coloration syntaxique.

# Problèmes rencontrés
Mais voila, du téléchargement d’Octopress à la publication sur Github, tout n’a pas été si simple. 
Heureusement, [le blog de David Tellander](http://derantell.github.io/blog/2012/12/02/getting-started-with-octopress-on-windows/) a répondu à la plupart de mes problèmes cités ci-dessous.

### > UTF-8 - Les accents
La gestion des accents n'a pas évidente :

* La commande rake generate échoue si un accent est présent dans la partie descriptive du post [YAML](http://fr.wikipedia.org/wiki/YAML ). J'ai donc du remplacer les lettres par leur [codes ISO](http://www.commentcamarche.net/contents/489-caracteres-speciaux-html).
* Pour que les accents s'affichent dans le corps du post, il m'a fallu encoder les posts en UTF-8 (sans [Byte Order Mark](http://en.wikipedia.org/wiki/Byte_order_mark#UTF-8) comme précisé dans [la documentation Jekyll](http://jekyllrb.com/docs/frontmatter/)  ).</br></br>

### > Windows - Commande inexistante
Au moment de déployer sur GitHub, le message suivant s'est affiché :
> *‘hellip’ is not recognized as an internal or external command, operable program or batch file.*

La correction a consisté à remplacer ```&hellip;``` par ```...``` dans le fichier ```RakeFile``` à la ligne suivante :
```
    system "echo 'My Octopress Page is coming soon &hellip' > index.html"
```
### > GitHub - HTTPS et les branches
Le client SSH étant absent de mon post, j'ai du modifier la variable *branch* du fichier ```Rakefile``` pour que l’expression régulière accepte les urls HTTPS au déploiement du blog ([corrigé le 1er juin 2013](https://github.com/imathis/octopress/commit/f5bb4dd89ea64181910acb8ef0df5ae84644b75d)).
Mais une fois l'URL acceptée, conséquence directe ou non, Octopress n'a jamais voulu publier sur une autre branche que *gh-pages* (Project Page) au lieu de master (Organization Pages). 
J'ai donc finalement préciser manuellement la branche dans le fichier ```Rakefile``` :
```
branch = 'master'
project = ''
```
  
### > Coloration synthaxique
La présence de la langue dans les blocs de code cassait systématiquement la génération du site :
```
''' java
public class Toto {
}
'''
```

En effet [Python (version 2.7.5)](http://www.python.org/download/releases/2.7.5/) est indispensable pour l'application de la coloration synthaxique.

# Ressources
La [documentation officielle](http://octopress.org/docs/) décrit étape par étape comment installer, rédiger et publier sur GitHub ou Heroku.
Pour les utilisateurs Windows, un tour sur [le blog de David Tellander](http://derantell.github.io/blog/2012/12/02/getting-started-with-octopress-on-windows/) vous évitera de vous arracher les cheveux.

#Conclusion

Pour l’instant, Octopress répond parfaitement à mes besoins. Je suis persuadé que si j’étais sous Linux ma première publication se serait passée plus simplement. 
Mais une fois tous les problèmes réglés, la publication d’un billet est un jeu d’enfant. Une communauté semble se développer autour du projet (Jekyll de manière plus générale) 
mais l’activité sur [GitHub](https://github.com/imathis/octopress) n’est pas dingue ces derniers temps.