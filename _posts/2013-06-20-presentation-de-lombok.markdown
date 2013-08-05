---
layout: post
title: "Pr&#233;sentation de Lombok"
date: 2013-06-20 09:29
comments: true
categories: [Java]
---
<img style="float : left;" src="{{ root_url }}/images/posts/lombok-logo.png" title="logo" />
[Lombok](http://projectlombok.org) est une API dont le but est de générer à la compilation, du code Java(*getters()/setters(), toString()...*), à notre place . 
Tout se fait à l'aide de simples annotations à poser dans nos classes. Actuellement en version [0.12 - Angry Butterfly](http://projectlombok.org/download.html), le projet est de plus en plus populaire.

<!--more-->
<div style="clear:both;"/>
<br/>

# L'API

Il existe de nombreuses annotations, dont certaines sont directement inspirées de Groovy. En voici une sélection...

### > @Getter et @Setter
Génère les getters/setters d'un attribut d'une classe :
{% codeblock  @Getter et @Setter lang:java %}
public class GetterSetterExample {
   @Getter 
   @Setter 
   private String name = "toto";
}
{% endcodeblock %}

Il est également possible de gérer un cache sur les getters avec [@Getter(lazy=true)](http://projectlombok.org/features/GetterLazy.html).

### > @ToString et @EqualsAndHashCode
Implémente respectivement les méthodes *toString(), equals()* et *hashCode()*

{% codeblock  @ToString et @EqualsAndHashCode lang:java %}
@EqualsAndHashCode
@ToString
public class ToStringEqualsAndHashCodeExample {
   @Getter 
   @Setter 
   private String name = "toto";
}
{% endcodeblock %}

Les deux annotations permettent également d'exclure certains attributs.

### > @Data
Combinaison de *@Getter,@Setter,@EqualsAndHashCode* et *@ToString*.
Les accesseurs et les méthodes *toString(), equals()* et *hashCode()* sont générées et disponibles à la complétion.

### > @Cleanup

Permet de fermer proprement une ressource ouverte sans avoir à écrire les blocs try{}/finally{}
{% codeblock  @Cleanup lang:java %}
@Cleanup InputStream in = new FileInputStream(args[0]);
{% endcodeblock %}

### > @Delegate
Directement inspirée de [Groovy](http://groovy.codehaus.org/Delegate+transformation), génère dans un objet A contenant B toutes les méthodes de B afin d'éviter de faire *A.getB().XXX*

{% codeblock @Delegate lang:java %}
@Data
public class A  {
   @Delegate
   private B b = new B();
}   

@Data
public class B  {
   private String name;
}   

{% endcodeblock %}

{% codeblock lang:java %}
new A().setName("toto");
{% endcodeblock %}

### > @Builder
Génère comme son nom l'indique un builder.

{% codeblock @Builder lang:java %}
@Builder
public class BuilderExample {
  private String name;
  private int age;
}
{% endcodeblock %}

{% codeblock lang:java %}
BuilderExample.builder().name("toto").age("age").build();
{% endcodeblock %}

### > @NonNull
Si *javax.validation.constraints.NotNull* existe déjà dans Java 6, elle ne fait qu'indiquer que le paramêtre ou la valeur retournée d'une méthode ne doivent pas être null.
Lombok propose une annotation similaire [lombok.NonNull](https://github.com/rzwitserloot/lombok/blob/master/src/core/lombok/NonNull.java) et **renvoie** une NullPointerException si besoin.

{% codeblock @NonNull lang:java %}
public NonNullExample(@NonNull Person person) {
	...
}
{% endcodeblock %}
Cela évite d'utiliser les [Preconditions de Guava](http://code.google.com/p/guava-libraries/wiki/PreconditionsExplained).

### > Experimentals
Quelques annotions sont dites "experimental" avant de rejoindre les "main" ou bien de disparaitre.
Elles sont référencées [ici](http://projectlombok.org/features/experimental/index.html). 
On y retrouve *@Builder* par exemple.

# Architecture
Le principe de Lombok est simple : juste avant la compilation , les fichiers sources sont parcourus afin remplacer les annotations par du code.
Si les annotions sont apparues avec Java 5, leur gestion à la compilation (**RetentionPolicy.SOURCE**) nécessitait l'appel à [Apt](http://docs.oracle.com/javase/1.5.0/docs/guide/apt/GettingStarted.html) avant l'appel à Javac. 
Avec l'arrivée de Java 6, le parcours des sources (Abstract Syntax Tree ou AST) est directement intégré au compilateur. De là est né ce projet.
Lombok s'appuie sur la <a href="http://www.jcp.org/en/jsr/detail?id=269">JSR 269 Pluggable Annotation Processing API</a> et nécessite obligatoirement le JDK 6 pour la compilation.

Le parcours de l'Abstract Syntax Tree est expliqué en détails sur [Java.net](https://www.java.net//pub/a/today/2008/04/10/source-code-analysis-using-java-6-compiler-apis.html#accessing-the-abstract-syntax-tree-the-compiler-tree-api).

# L'installation

### > Projet Maven
 
{% codeblock pom.xml lang:xml  %}
...
<dependencies>
...
	<dependency>
		<groupId>org.projectlombok</groupId>
		<artifactId>lombok</artifactId>
		<version>0.11.8</version>
		<scope>provided</scope>
	</dependency>
...
</dependencies>
...
{% endcodeblock %}
Ne pas oublier que Lombok requiert Java 6 au minimum dans la configuration du plugin de compilation :
{% codeblock pom.xml lang:xml  %}
...
<plugins>
...
	<plugin>
		<artifactId>maven-compiler-plugin</artifactId>
		<version>${maven-compiler-plugin.version}</version>
		<configuration>
			<source>1.6</source>
			<target>1.6</target>
		</configuration>
	</plugin>
...
</plugins>
...
{% endcodeblock %}

### > IDE
Pour que les méthodes générées automatiquement à la compilation soient disponibles à la complétion dans notre IDE, il est nécessaire d'installer un plugin.
Loombock est compatible avec NetBeans, Eclipse (et ses variantes) et IntelliJ.

#### Eclipse
Le support d'Eclipse est assuré par l'équipe même du projet.
Une fois lombock dans les dépendances de l'application, il suffit de faire *Run as Application* et choisir la classe *lombok.core.Main.class*
<img src="{{ root_url }}/images/posts/lombok-setup-eclipse.png" />

En cliquand sur *install/update*, Lombok met à jour le fichier *eclipse.ini*
{% codeblock %}
-javaagent:lombok.jar
-Xbootclasspath/a:lombok.jar
{% endcodeblock %}

#### > IDEA IntelliJ
Le plugin est hébergé sur [Google Code](https://code.google.com/p/lombok-intellij-plugin/).
Son installation se limité au dézippage de l'[archive](https://code.google.com/p/lombok-intellij-plugin/downloads/list) dans le répertoire ```/plugins```.
La version du plugin dépend de la version d'IntelliJ installée.

#### > Netbeans
Il suffit de cocher *Enable Annotation Processing in Editor* dans les propriétés du projet (http://projectlombok.org/setup/netbeans.html)

# Delombok

Il est important de garder à l'esprit que la génération de code se fait à la compilation. 
Tous les outils qui se basent sur le code source de nos projets ne verront que les annotations Lombok. 
C'est pourquoi la JavaDoc générée est imcomplète car Lombok n'a pas encore mis à jour les sources.

L'équipe du projet a inclu dans *lombok.jar*, l'outil *delombok* qui copie les sources modifiées dans le répertoire de son choix.
L'interêt est double : il permet d'apercevoir le code généré mais également d'indiquer ce répertoire à la génération de la JavaDoc afin que toutes les méthodes y soient référencées.

Delombok est à la fois compatible avec Ant ([http://projectlombok.org/features/delombok.html](http://projectlombok.org/features/delombok.html)) et Maven ([http://awhitford.github.com/lombok.maven/](http://awhitford.github.com/lombok.maven/)).

# GWT 

Lombok semble compatible avec GWT. 
Malheureusement je reste sur un échec.
https://groups.google.com/forum/#!topic/project-lombok/WwiymShYBsg

# Conclusion

A consommer sans modération !

# Les ressources

* Projet Lombok - [http://projectlombok.org](http://projectlombok.org)
* Documentation - [http://projectlombok.org/api/index.html](http://projectlombok.org/api/index.html)
* Projet GitHub - [https://github.com/rzwitserloot/lombok](https://github.com/rzwitserloot/lombok)

http://notatube.blogspot.fr/2010/12/project-lombok-creating-custom.html
http://jnb.ociweb.com/jnb/jnbJan2010.html
