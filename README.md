# Installation et personnalisation d'un générateur de site statique

Cet exercice constite à mettre en place une solution de publication web statique basé sur la [Jamstack](https://jamstack.org/what-is-jamstack).

La [stack](https://fr.wiktionary.org/wiki/stack) (ensemble de composants logiciels) généralement utilisée pour la mise en œuvre d'un site statique est la suivante :

 - un service d'hébergment et de versionnage du code source ([GIT](https://fr.wikipedia.org/wiki/Git));
 - un service de gestion de contenu (CMS)
 - un service d'hebergement [CDN](https://fr.wikipedia.org/wiki/R%C3%A9seau_de_diffusion_de_contenu);
 - générateur de site statique ;

Dans le cadre de cet exercice; **Le service de versionage du code source** utilisé sera [Github](github.com), **la gestion de contenu** sera assurée sur [Forestry](forestry.io), **l'hébergement CDN** sur [Vercel](vercel.com) et **le générateur statique** utilisé sera [Gridsome](gridsome.org).

Un compte Gihub est nécessaire pour ce cours, les autres service pourrons vous authentifier au travers de votre compte Github.

Note : 
Cet exercice est une adapatation de [l'exercice sur le générateur de site statique Hugo](https://github.com/ziopod/nws-hugo-cms) pour Gridsome.

## Installation de la stack

Bien qu'il y ait diverses manières de mettre en place une Jamstack, les services cités sont des solutions spécialisées dans la conception de site statique. Ainsi, ces services proposent des méthodes simplifiées pour mettre en place ce type de site web. Voyons ça étape par étape.

### Grisome & Github via Forestry

Forestry est un CMS dédié aux générateur de site statique, il nous offre la possibilité d'utiliser une procédure automatisé pour configurer Forestry, installer un générateur de site statique et d'y associer un thème.

**Prérequis** : un compte [Github](github.com).

Pour commencer, nous allons sélectionner un pack de démarrage sur Forestry via la page https://forestry.io/starters.

Choisissez « Gridsome » dans les filtres, puis le thème « Unstad », cliquez sur la flêche, puis sur « Grisome ». Autrement, vous pouvez passer par le lien de déploiement depuis la documentation du thème : https://github.com/itsnwa/gridsome-forestry-starter

Une fenêtre s'ouvre vous proposant de choisir l'hébergement GIT, nous choisirons Github et un nom explicite pour le dépôt (par exemple « debuter-avec-gridsome »).

Cliquez sur « Import to Forestry », à partir de là, Forestry créer un dépôt Github pour vous et y installe Gridsome ainsi que le thème « Unstad ».

Une fois la procédure terminée, vous êtes redirigé sur l'interface d'administration du CMS. Vous constaterez qu'un contenu par défaut est présent. Jetez un œil également au dépôt Github qui viens d'être créer (par exemple https://github.com/votre-nom-utilisateur/debuter-avec-gridsome).

### Environnement de travail local

Pour travailler confortablement sur votre projet web, l'idéal est bien entendu d'avoir les fichiers à disposition localement et d'afficher le site sur un serveur de développement local.

**Prérequis** : un environnement local [NodeJS](nodejs.org)

Gridsome est générateur de site statique basé sur le framework [Vue.js](vuejs.org), pour fonctionnement localement, il est nécessaire d'avoir [installé un environnement NodeJS](https://nodejs.org/en/download). Assurez-vous d'avoir une version LTS (Long Term Support) à jour. Via votre terminal ([interface système Shell](https://fr.wikipedia.org/wiki/Interface_syst%C3%A8me)), vous pouvez contrôler la version avec la commande suivante : 
~~~
$ node --version
~~~

La réponse devrais être quelque chose comme `V14.15.1`.

Faîte une copie local de votre dépôt, soit via le logiciel [Github Desktop](https://desktop.github.com) ou, si [GIT est installé sur votre machine](https://git-scm.com/downloads), via la ligne de commande suivante : 

~~~
$ cd /chemin/vers/le/dossier/de/votre/projet/
$ git clone https://github.com/votre-nom-utilisateur/debuter-avec-gridsome 
~~~

Via votre terminal, rendez-vous dans le repertoire de votre dépôt : 
~~~
$ cd debuter-avec-gridsome/
~~~

Installer les dépendances du projet avec la commande :
~~~
$ npm install
~~~

Puis lancez le serveur local de Gridsome avec la commande :
~~~
$ npm run develop
~~~

Vous devriez voir un message qui ressemble à ceci : 
~~~
Gridsome v0.7.20

Initializing plugins...
Load sources - 0.2s
Create GraphQL schema - 0.1s
Create pages and templates - 0.07s
Generate temporary code - 0.29s
Bootstrap finish - 9.44s


 DONE  Compiled successfully in 9569ms                                                                                                                             18:09:58


  Site running at:                                         
  - Local:                 http://localhost:8081/          
  - Network:               http://192.168.1.17:8081/       
                                                           
  Explore GraphQL data at: http://localhost:8081/___explore
~~~

Le message nous indique que la compilation à été effectuée correctement. Vous remarquez trois URL : 

 - **Local** : c'est l'addresse du serveur local de votre machine ;
 - **Network** : il s'agit de l'adresse de réseau de votre serveur local ;
 - **GraphQL** : affiche une interface pour explorer les données de votre site.

Nous utiliserons essentiellement **l'adresse locale**, saissisez-là dans la barre d'adresse de votre navigateur pour afficher votre site local.

L'**adresse réseau** permet d'afficher votre site local sur un périphérique relié au même réseau que votre machine locale (via le Wifi par ex.). Si vous avez un smartphone relié au même réseau que votre ordinateur, vous pouvez afficher votre site dessus en saissant l'adresse dans le navigateur de votre smartphone.

Explorer les données **GraphQL** permettras de comprendre et de tester l'accès aux données (ce qui est essentiel lorsque que l'on veut développer ou ajouter des pages aux thèmes).

À ce stade, si vous modifez le code source ou les données, celle-ce seront automatiquement affichés sur les divers périphériques (hot reloading).

### Hébergemement sur Vercel

Un générateur de site statique possède une commande qui construit (build) le site statique, le principe est de compiler et d'optimiser tout les fichiers constituant le site et de les mettre à disposition dans un répertoire (nommé `dist`, `build`, `_site` en fonction du générateur de site statique).

Avec gridsome, vous pouvez construire votre site avec la commande suivante :
~~~
$ npm run build
~~~

Une fois la procédure terminée, vous pouvez constater la création d'un repertoire `dist` contenant tous les fichiers de votre site compilé.

Ce répertoire pourras être mis à disposition des internautes sur un serveur web (c'est ce que l'on appel le déploiement). À chaque mise à jour de contenu (un nouvel article de blog via le CMS par exemple), il faut de nouveau construire le site et le mettre à dispositon des internautes.

Bien entendu, nous n'allons pas nous amuser à faire cela manuellement à chaque fois que le contenu est modifié, nous allons automatiser le déploiement du site (technique dite du « [déploiement continue](https://fr.wikipedia.org/wiki/D%C3%A9ploiement_continu) »).

Il vas s'agir de configurer un serveur virtuel pour construire le site, puis de transférez le résultat sur le serveur HTTP, c'est une étape qui normalement réclame des compétences d'[administateur système](https://fr.wikipedia.org/wiki/Administrateur_syst%C3%A8me). Fort heuresement, Vercel nous popose de une méthode simplifié, rendez-vous sur https://vercel.com, puis connectez-vous avec votre compte Github.

Une fois sur votre tableau de bord Vercel, cliquez sur « Import Project », choisissez « Import Git Repository » (cliquez sur « continue »); puis indiquez l'adresse du dépôt Git de votre projet (par exemple : https://github.com/votre-nom-utilisateur/debuter-avec-gridsome) et « Continue ».

À ce stade, vous pouvez obtenir un **message d'erreur** vous indiquant que Vercel ne peut pas accéder à votre projet. Dans ce cas il faut autoriser Vercel à communiquer avec votre compte Github, suivez le lien indiqué dans le message d'erreur de Vercel. Celui-ci vous inviteras à suivre les étapes nécessaire à la configuration de votre compte Github. (plus d'[informations sur Github & Vercel](https://vercel.com/docs/git/vercel-for-github))

Une interface de configuration vous est proposé, laissez tout par défaut, cliquez sur « Deploy ». Vous devriez voir une interface afficher le processus du build en cours. Un fois le processsus terminé, un lien vous invite à visiter votre site en production. vous devriez obtenir le même rendu que votre site Local.

À partir de maintenant votre Jamstack est parfaitement opérationnelle.

Remarquez que Vercel genère un sous-domaine pour accéder au site en production, vous pouvez personnaliser l'adresse via les réglages depuis votre projet via « Settings > Domains». C'est via cet interface que vous pouvez rattacher un nom de domaine réservé pour votre projet.

## Personnalisation du site

À ce stade, toutes les modifications qui seront engagées sur le dépôt Github (code source modifié ou contenu modifié via Forestry) provoquerons une nouvelle construction automatique du site, puis une [mise en production](https://fr.wikipedia.org/wiki/Environnement_(informatique)). Nous avons mis en place une pratique moderne  de génie logiciel (méthode « agile » d'[Extreme Progamming (XP)](https://fr.wikipedia.org/wiki/Extreme_programming) ) que l'on appelle [l'intégration et le déploiement continue](https://fr.wikipedia.org/wiki/Int%C3%A9gration_continue) ([CI/CD](https://en.wikipedia.org/wiki/CI/CD)).

Avant de personnaliser le thème, découvrons la structure des répertoires d'un projet Gridsome.

### Structure des répertoires

Dans un premier temps, intéressons nous au **fichier de configuration de Gridsome**. Dans ce fichier, nous allons personnaliser l'URL, le nom, la description et le format des titre méta du site. Pour aller plus loin, consultez [la documentation sur la configuration d'un projet Gridsome](https://gridsome.org/docs/config/).

le repertoire `node_modules` héberge les dependances NodeJS pour notre projet, nous n'interviendrons jamais directement dessus.

Les fichiers source qui contiendrons la logique, le code de balisage HTML et le code de présentation CSS seront placés dans le répertoire `src`, les fichiers "passifs" accompagnant le site seront à mettre dans le répertoire `static` (comme le favicon ou le logo du site par exemple).

Notez également la présence du repertoire `dist` et `.cache` si vous avez éxécuté un build. Le repertoire `dist` contient la version de production fonctionelle de votre dernier build  prêt à être mis en ligne.

Les autres repertoires présent sont pour la gestion de contenu, un repertoire `.forestry` qui contient la configuration de l'interface d'administration de forestry et les répertoires `data`, `journal`, `projects` et `uploads` pour les fichiers de contenu. Notez qu'il est courant des regroupé tout les repertoires de contenu dans un  repertoire principal que l'on nomme `content`. Dans le cas de [notre thème](https://github.com/itsnwa/gridsome-forestry-starter) [le designer Itsnwa](https://github.com/itsnwa) à fait un autre choix d'agencement.

### Le templating de Gridsome

Dans le repertoire `src`, Gridsome propose d'organiser les repertoires de [templating](https://fr.wiktionary.org/wiki/templating) Vue.js de cette manière : 

 - `assets` : les fichier externes à inclure au HTML (fichiers CSS principal par exemple) ;
 - `layouts` : les fichiers "maître" du site, les autres fichiers seront inclus dans un fichier layout ;
 - `pages` : représente la page servie à une URL spécifique du site, par exemple à l'URL `/contact` correspondras le fichier `Contact.vue` ;
 - `templates` : représente un conteneur pour les URL "dynamique", par exemple un article du journal (donnée de type `JournalPost`), sera servie à l'URL `/journal/slug-de-l-article`, les données de cet article (titre, contenu, etc) sera à disposition du fichier `JournalPost.vue`.
 - `components` : contients [les composants Vue.js](https://vuejs.org/v2/guide/components-registration.html#Local-Registration-in-a-Module-System), ce sont des élements de  l'interface du site web que l'on peut ré-employer n'importe ou sur le site (comme l'en-tête de navigation du site ou un bouton cliquable par exemple).

Nous sommes dans un environnement typique de Vue.js. Bien entendu, le but ici ne vas pas être d'écrire notre propre thème en Vue (je vous rassure), mais simplement de pouvoir suffisament s'y retrouver afin d'y apporter les modifications qui nous conviennent. Voyons maitenant de quoi est constitué un fichier Vue.js

## Gridsome est construit avec Vue.js

Gridsome est basé sur le framework Vue.js, les notions abordé dans ces chapitres sont documentées sur https://fr.vuejs.org.

Pour se faciliter la tâche, n'hésitez pas installer une extension de coloration syntaxique et d'auto-complétion pour Vue.js à votre IDE. Voici celui à installer pour Visual Studio Code : [Vetur](https://marketplace.visualstudio.com/items?itemName=octref.vetur)

### Description du layout principal

Jettons un œil au fichier situé à `src/layouts/Default.vue`. Celui-ci sera chargé pour toutes les URL du site, il chargeras d'autre éléments Vue.js en focntion du contexte de l'URL.

Sur ce fichier, nous observons trois marqueurs Vue.js typique : 
 - `<template>` pour placer les marqueurs HTML et la logique d'affichage ;
 - `<script>` qui sert à écrire les fonctionnalités Javascript ;
 - `<style>`qui sert à écrire le code de présentation CSS.

Détaillons un peu, nous avons observons les marqueurs de templates `<Header/>` et `<Footer/>`, ce sont des composants Vue, ils servent à inclure les éléments de template  `src/components/Header.vue` et `src/components/Footer.vue`.

#### Le slot

Ensuite le marqueur `<slot/>`, il désigne l'emplacement ou sera encaspulé les autes fichiers Vue. Ces fichiers Vue seront désigné en fonction du contexte d'URL.

Pour bien comprendre le rôle de `<slot/>`, voyons un exemple complet :

Si l'on sollicite la route `http://localhost:8081/contact`, le système de routes de Gridsome vas solliciter le fichier `src/pages/Contact.vue`, si l'on regarde le code de ce fichier `Contact.vue`, nous observons une paire de marqueurs ouvrant/fermant `<Layout></Layout>` qui encadre le code source de cette page, ce marquer indique au système que cette page `Contact.vue` doit être chargé à la place du marqueur `<slot/>` du fichier de layout (`src/layouts/Default.vue`).


#### Le contenu HTML

Le première balise `div` du template sert à contenir tout les autres marqueur de template (`<template>` n'accepte qu'un seul enfant). Cette balise contient un attribut de classe HTML `class` classique et un autre précedé d'un deux-points `:`. Ce signe deux-point `:` signifie à Vue d'interpréter en Javascript le code spécifié en valeur de l'attribut (entre la paire de guillemets `""`). Le code `{ 'sticky-header': $route.path === '/' }` sera donc interprété comme du Javascript, ce code est une structure conditionnelle qui vas ajouter la classe CSS `sticky-header` lorsque que l'on sera sur la page d'accueil.

Le code `<div class="layout" :class="{ 'sticky-header': $route.path === '/' }">`, ce

#### Le marqueur pour le code logique Javascript

La marqueur `<script>` sert à écrire le code logique pour l'application.


Comme nous utilisons des componsants dans ce fichier, il est nécessaire de les instancier.

Pour cela, nous importons le module composant avec la directive `import`, puis le déclarons via la propriété de [module Javascript](https://developer.mozilla.org/fr/docs/Web/JavaScript/Guide/Modules) `components`. Notez qu'il est de coutume d'utiliser une [notation en camel case](https://en.wikipedia.org/wiki/Camel_case) pour les modules Javascript.

#### Le marqueur de style CSS

Finalement le marqueur `<style>` qui sert çà definir un CSS qui sera disponible pour toutes les pages du site.

### Personnalisation du layout principal

Comme ce layout est affiché à chaque page, nous pouvons y spécifier le style global du site. 

Personalisons la typographie du site, dans la balise `<style>`, modifions le selecteur CSS `body` :  

~~~
body {
  --color-base: rgb(255, 255, 255);
  --color-base-1: rgb(243, 243, 243);
  --color-contrast: rgb(0, 0, 0);
  --color-contrast-1: rgb(43, 43, 43);
  --font-size: 1em;
  font-family: "PT Sans", Arial, sans-serif;
  margin:0;
  padding: 0;
  font-size: var(--font-size);
  line-height: 1.5em;
  background: var(--color-base);
  color: var(--color-contrast);
  transition: background 0.5s ease;
}
~~~

Nous avons spécifié la famille de fonte `PT Sans`, cette typo ne sera probablement pas disponible sur la machine locale l'utilisateur.

Nous devons indiqué à CSS de la charger depuis un service externe (Google Webfont) grâce à [la directive CSS `@font-face`](https://developer.mozilla.org/fr/docs/Web/CSS/@font-face) : 

~~~
@font-face {
  font-family: "PT Serif";
  font-display: auto;
  src: local('PT Serif'), url('https://fonts.googleapis.com/css2?family=PT+Serif:wght@700&display=swap') format('woff2');
}
@font-face {
  font-family: "PT Sans";
  font-display: fallback;
  src: local('PT Sans'), url('https://fonts.googleapis.com/css2?family=PT+Sans:ital,wght@0,400;0,700;1,400&display=swap') format('woff2');
}
~~~



Nous avons également ajouté une variable CSS `--font-size` pour géré la taille de corps.

Cette variable de taille de corps, vas nous permettre de modfifier la taille de corps général en fonction du support d'affichage. Nous voulons un taille de corps plus grande lors d'un affichage tablette et écran d'ordinateur. un selecteur `@media` pour les tablettes et les écran d'ordinateurs est déjà présent, exploitons-le : 

~~~
@media (min-width: 860px) {
  body {
    --font-size: 1.312em;
  }
  .container {
    padding: 0 6rem;
  }
}
~~~

Nous avons modifié la valeur de la variable `--font-size` pour la balise HTML `body` et toutes ses balises descendatnes lorsque la page sera affiché sur un support d'au moins 860px de large (`min-width: 860px`).

Pour que cet astuce d'héritage de taille de corps fonctionne correctement sur ce thème, il est nécessaire de **modifier toutes les unités de mesures `rem` des propriétés `font-size`** par des l'unité `em`.

Par exemple, dans le fichier du pied de page `src/components/Footer.vue`, passer `font-size: 0.8rem` à `font-size: 0.8em` : 

~~~
.footer {
    font-size: 0.8em;
    padding: 6rem 0;
}
~~~

Passez en revue tous les fichiers du repertoire `src` et corrigez toutes les unités de mesure `rem` des propriétés CSS `font-size` que vous trouverez.

### Création d'un composant Vue

En faisant le tour des fichiers `.vue`, nous voyons bien que le site est découpé sous forme de petits "morceaux" ré-employable, il s'agit de [modules Vue.js](https://fr.vuejs.org/v2/guide/components-registration.html#Systemes-de-module).

Ajoutons notre propre module.

Dans le repertoire `src/components` créez un fichier `Button.vue`, éditez ce fichier comme ceci : 

~~~
<template>
  <a class="button">
    <slot/> ❯
  </a>
</template>

<style>
.button {
  display: inline-block;
  text-transform: uppercase;
  text-decoration: none;
  padding: .75em 1em;
}
.is-dark {
  background: black;
  color: white;
}
</style>
~~~

Mis à part le marqueur de template `<template>` pour délimiter le HTML, le reste se comorte comme du HTML / CSS classique.

Remarquez le marqueur `<slot/>`, [les slots de Vue]( https://fr.vuejs.org/v2/guide/components.html#Distribution-de-contenu-avec-les-slots) servent à distribuer du contenu, celui-ci sera remplacer par du texte que l'on pourras spécifier lors de l'usage de ce composant (comme pour `<Layout></Layout>`).

Illustrons l'usage de ce composant en l'affichant dans le bandeau héro de la page d'accueil. Le héro est représenté par le fichier `src/components/Hero.vue`, ajoutons notre bouton sous le texte d'introduction :

Dans la partie `<script>`, il est nécessaire d'importer le bouton avec [l'instruction `ìmport`](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Instructions/import) et de le déclarer comme composant dans la propriété `components` :

~~~
<script>
import Button from '@/components/Elements/Button'

export default {
  components: {
    Button
  },
  data() {
    return {
      settings: require("../../data/theme.json")
    }
  }
}
</script>
~~~

Nous pouvons maintenant l'utiliser dans le template :
~~~
<template>
    <div class="hero">
        <h1 class="hero-title" v-html="settings.hero_title" />
        <h2 class="hero-subtitle" v-html="settings.hero_subtitle" />
        <Button
          href="/journal/gridsome-forestry-cms"
          class="is-dark"
        >Lire cet article</Button>
    </div>
</template>
~~~

Remarquez les attributs `href` et `class`, ceux-ci seront transmis au composant `Button`. La valeur `is-dark` de `class` sera ajouté à la valeur initiale de l'attribut `class` du composant. Nous avions déclarez `<button class="button">` en valeur initiale, un fois le tout compilé, nous obtiendrons `<button class="button is-dark">`. Le texte `Lire cet article` sera inséré à la place du marqueur `<slot/>` (notez bien que le marqueur `slot` s'écrit tout en minuscule).

Vous pouvez maintenant ré-employer ce composant à volonté avec divers paramètres.

### Allez plus loin avec Vue.js

Avec ces notions de base et en s'appuyant sur les fonctionnalités existantes d'un thème, il est possible de mettre en place de grande choses.

Vue.js s'articule pleinement autours de ce système de composants, en prenant le temps de se documenter, il est possibles d'ajouter rapidement des fonctionnalité très utiles.

J'ai glissé un petit exemple de fenêtre de notifications éditables dans Forestry et qui possède une fonctionnalité d'état de l'affichage qui reste enregistré localement sur le navigateur client. Cette exemple est entièrement documenté dans le code source si vous désirez le reproduire.

Fichiers du composant : 
 - `src/components/Elements/Notifications.vue`
 - `src/components/Elements/Close.vue`

L'exemple d'usage est situé dans le fichier `src/layouts/Header.vue`.

Pour pouvoir gérer les notifications via Forestry, il faut éditer le fichier `.forestry/front_matter/tempaltes/theme-configuration.yml`, et ajouter la configuration suivante à la propriété `fields:` :

~~~
- name: notifications
  type: field_group_list
  fields:
  - name: id
    type: text
    config:
      required: true
      max: 255
    label: Id
  - name: message
    type: text
    config:
      required: true
    label: Message
  - name: color
    type: select
    default: []
    config:
      required: false
      options:
      - is-info
      - is-warning
      source:
        type: simple
        section: 
        file: 
        path: 
    label: color
  config:
    min: 
    max: 3
    labelField: id
  label: Notifications
~~~
