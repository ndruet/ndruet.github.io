---
layout: post
title: "Cr&#233;er un blog avec Octopress sous Windows"
date: 2013-05-27 16:47
comments: true
categories: [Octopress]
---

L'ouverture de ce blog aura été l'occasion de découvrir [Octopress](http://octopress.org), un générateur de blog statique écrit en Ruby basé sur [JeKyll](http://jekyllrb.com).

<img class="middle" src="{{ root_url }}/images/posts/octopress-logo.png" title="logo" >

<!--more-->

# Simple<a name="Simple"></a>
L’avantage principal d’un générateur de blog statique, en comparaison avec Wordpress ou Blogger, est sa simplicité de fonctionnement. 
Aucune base de données n'est nécessaire, ni de serveur d’application. 
Le blog tient la charge même avec une forte audience, répond rapidement, et surtout se teste facilement en local.

Les principales commandes d'Octopress sont :

{% codeblock %}
rake generate          # Genère entièrement le site à partir du fichier _config.xml et les répertoires /sources et /saas
rake preview           # Monte un serveur http://localhost:4000 et prend à chaud les modifications des posts (/sources)
rake new_post["title"] # Création d'un nouveau post
rake deploy            # Déploiement sur GitHub
{% endcodeblock %}
Par défaut les articles suivent la synthaxe [Markdown](http://daringfireball.net/projects/markdown/) et s'éditent avec un simple éditeur de texte (Notepad++ en l'occurence).

# Thèmes<a name="Thèmes"></a>
Les thèmes sont disponibles sur GitHub, et apportent en général une présentation claire, et sont +/- *responsive design*.

L'installation se résume à ces quelques commandes :
{% codeblock %}
cd octopress                         # Se placer à la racine d'Octopress
git clone GIT_URL .themes/THEME_NAME # Clone le repo du thème et lui affecte un nom
rake install['THEME_NAME']           # Installe le thème
rake generate                        # Regénère le blog
{% endcodeblock %}

La commande ```rake install``` permet de switcher d'un thème à l'autre.

Vous en trouverez sur [http://octopressthemes.com](http://octopressthemes.com/) et sur [le wiki](https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes).
Si le thème par défaut suffit amplement et ne nécessite pas de modification, l'idée d'avoir la main sur le CSS et les templates est plutôt agréable.
Personnellement, j'ai opté pour [Foxslide](https://github.com/sevenadrian/foxslide).

# Plugins<a name="Plugins"></a>
Octopress inclut quelques plugins prêts à l'emploi. 
Ainsi l'interfaçage avec les comptes twitter, google+, google analytics… s'effectue en renseignement ses identifiants dans le fichier ```_config.xml```.
On peut également inclure des Gists, des videos HTML5, bénéficier de la coloration syntaxique et ajouter DISQUS pour les commentaires.

D'autres existent et sont listés sur le [wiki](https://github.com/imathis/octopress/wiki/3rd-party-plugins).

# Problèmes rencontrés<a name="Problèmes rencontrés"></a>
Mais voila, du téléchargement d’Octopress à la publication sur Github, tout n’a pas été si simple. 
Heureusement, [le blog de David Tellander](http://derantell.github.io/blog/2012/12/02/getting-started-with-octopress-on-windows/) a répondu à la plupart de mes problèmes cités ci-dessous.

### > UTF-8 - Les accents
La gestion des accents n'a pas été évidente :

* La commande ```rake generate``` échoue systématiquement si un accent est présent dans la partie descriptive du post [YAML](http://fr.wikipedia.org/wiki/YAML ). 
Il faut donc remplacer les caractères accentués par leur [codes ISO](http://www.commentcamarche.net/contents/489-caracteres-speciaux-html).
* Pour l'affichage des accents dans le corps du post, il est nécessaire d'encoder les posts en UTF-8 (sans [Byte Order Mark](http://en.wikipedia.org/wiki/Byte_order_mark#UTF-8) comme précisé dans [la documentation Jekyll](http://jekyllrb.com/docs/frontmatter/)).
</br></br>

### > Windows - Commande inéxistante
Au moment de déployer sur GitHub, le message suivant s'est affiché :
> *‘hellip’ is not recognized as an internal or external command, operable program or batch file.*

La correction consiste à remplacer ```&hellip;``` par ```...``` dans le fichier ```RakeFile``` à la ligne suivante :
{% codeblock %}
    system "echo 'My Octopress Page is coming soon &hellip' > index.html"
{% endcodeblock %}

### > GitHub - HTTPS et les branches
N'ayant pas de Client SSH d'installé sur mon PC, j'ai du modifier la variable *branch* du fichier ```Rakefile``` pour que l’expression régulière accepte les urls HTTPS au déploiement du blog ([corrigé le 1er juin 2013](https://github.com/imathis/octopress/commit/f5bb4dd89ea64181910acb8ef0df5ae84644b75d)).
Mais une fois l'URL acceptée, conséquence directe ou non, Octopress n'a jamais voulu publier sur une autre branche que *gh-pages* (Project Page) au lieu de master (Organization Pages). 
J'ai donc finalement précisé manuellement la branche dans le fichier ```Rakefile``` :
{% codeblock %}
branch = 'master'
project = ''
{% endcodeblock %}

### > Coloration synthaxique
La présence de la langue dans les blocs de code cassait systématiquement la génération du site :
{% codeblock %}
''' java
public class Toto {
}
'''
{% endcodeblock %}

L'installation de [Python (version 2.7.5)](http://www.python.org/download/releases/2.7.5/) a corrigé le problème.

### > Majuscule à chaque mot dans le titre du post
Ce n'est pas un bug mais un fonctionnement par défaut. 
Chaque mot contenu dans le titre débutait par une majuscule.
Pour éviter ce comportement, il est nécessaire de mettre à *false* l'attribut *titlecase* du fichier ```config.xml```.

### > Table des matières
Pour terminer, j'avais imaginé que la génération des indexs dans les posts (la table des matières) aurait été automatisé.
Malheureusement, il est nécessaire de passer par des plugins :

* [http://blog.riemann.cc/2013/04/10/table-of-contents-in-octopress/](http://brizzled.clapper.org/blog/2012/02/04/generating-a-table-of-contents-in-octopress/)
* [http://brizzled.clapper.org/blog/2012/02/04/generating-a-table-of-contents-in-octopress/](http://brizzled.clapper.org/blog/2012/02/04/generating-a-table-of-contents-in-octopress/)

# Ressources
La [documentation officielle](http://octopress.org/docs/) décrit étape par étape comment installer, rédiger et publier sur GitHub ou Heroku.
Pour les utilisateurs Windows, un tour sur [le blog de David Tellander](http://derantell.github.io/blog/2012/12/02/getting-started-with-octopress-on-windows/) vous évitera de vous arracher les cheveux.

#Conclusion

Pour l’instant, Octopress répond parfaitement à mes besoins.
Je ne regrette pas une seconde délaissé Worpress ou Blogger.
Si ma première publication n'a pas été simple, la publication d’un billet aujourd'hui est un jeu d’enfant. 
Une communauté semble se développer autour du projet et de Jekyll de manière générale. 
Si l’activité sur [GitHub](https://github.com/imathis/octopress) n’est pas dingue ces derniers temps, une [version 3.0](https://github.com/imathis/octopress/tree/3.0) semble se profiler à l'horizon.