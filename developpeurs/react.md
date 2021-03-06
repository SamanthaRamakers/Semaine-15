<!-- omit in toc -->
# React.js

- [Préambule](#préambule)
- [Installation](#installation)
- [Pourquoi utiliser React.js](#pourquoi-utiliser-reactjs)
- [Petit lexique](#petit-lexique)
  - [JSX](#jsx)
  - [ReactDOM et Render()](#reactdom-et-render)
  - [Import React](#import-react)
  - [React Components](#react-components)
    - [JSX Capitalization](#jsx-capitalization)
  - [Components Interacting](#components-interacting)
    - [Props](#props)
    - [Constructor](#constructor)
    - [State](#state)
  - [Lifecycle Methods](#lifecycle-methods)
  - [Hooks](#hooks)

## Préambule

React est une bibliothèque JavaScript pour construire des interfaces utilisateurs. Le principe est de composer des UI complexes à partir de composants (bout de code isolés).

Avant de commencer il est de bon ton de relire un peu [la théorie JavaScript](https://developer.mozilla.org/fr/docs/Web/JavaScript/Une_r%C3%A9introduction_%C3%A0_JavaScript). Il n'est pas nécessaire d'être un pro du JS pour utiliser React, mais quelques bases sont tout de même recommandées.

Pour ce cours je vous suggère de suivre le [tutoriel officiel](https://fr.reactjs.org/tutorial/tutorial.html) de React qui est super bien fait et en français!

[:arrow_up: Revenir au top](#reactjs)

## Installation

1. Assurez-vous d'avoir Node d'installé.
2. Exécutez la commande suivante dans votre répertoire principal. Cela va créer une structure de base pour votre projet dans le dossier `mon-app`.

```bash
npx create-react-app mon-app
cd mon-app
npm start
```

3. Cliquez sur l'adresse local pour voir votre application.

[:arrow_up: Revenir au top](#reactjs)

## Pourquoi utiliser React.js

React est *rapide*. Une app réalisé avec React est capable de faire des mises à jour complexe et toujours être rapide et responsive.

React est *modulable*. A la place d'écrire de longue ligne de code, vous pouvez écrire des plus petites et des réutilisables.

React *évolutif*. Il s'adapte à tous type de projet et excelle sur les plus conséquent.

React est *flexible*. Il peut tout à fait servir à des projets qui n'ont rien à voir avec des app web.

react est *populaire*. Ce qui fait qu'il est plus facile de trouver de l'aide en ligne et également un job par après.

[:arrow_up: Revenir au top](#reactjs)

## Petit lexique

### JSX

Il s'agit d'une extension de syntaxe pour JavaScript. JSX à été créé pour React et ressemble à de l'HTML. Cependant il n'est pas du JS valide, le navigateur ne peut pas le lire. Ce qui veut dire qu'avant que du JSX puis arriver au navigateur, il va falloir le compiler. C'est ce que ferra React pour nous.

```html
<h1>Hello World</h1>
```

Ceci est une balise HTML tout à fait classique, mais si elle est dans un fichier .js alors c'est du JSX!

Les éléments JSX sont comme les expressions JS, ils peuvent être stockés n'importe où où une expression JS serait stockée, comme dans une variable, passé à une fonction, stocké dans un objet ou un tableau,...

```js
const navBar = <nav>I am a nav bar</nav>;

const myTeam = {
  js: <li>Julie</li>,
  css: <li>James</li>,
  photo: <li>Chris</li>,
  coms: <li>David</li>,
  boss: <li>Vincent</li>,
};
```

Il est tout a fait possible de donner des attributs à nos éléments JSX comme en HTML.

```js
const cat = <img src="img/cat.jpg" alt="cat" width="500px" height="350px" />
```

Il est également possible d'utiliser le nesting d'éléments JSX. Notez que si l'élément contient plusieurs lignes alors il faut placer le code entre parenthèses. Le tout peut évidement être enregistré dans une variable.

```js
 const theExample = (
   <a href="https://www.example.com">
     <h1>
       Click me!
     </h1>
   </a>
 );
 ```

:exclamation::exclamation::exclamation: Un point super important que l'on oublie souvent et qui est source de nombreuse erreur de compilation. Il faut que votre élément JSX ait un et un seul élément qui englobe tous les autres.

Le code suivant ne fonctionnera pas:

```js
const paragraphs = (
  <p>I am a paragraph.</p> 
  <p>I, too, am a paragraph.</p>
);
```

Tandis que celui-ci fonctionnera à merveille.

```js
const paragraphs = (
  <div id="i-am-the-outermost-element">
    <p>I am a paragraph.</p>
    <p>I, too, am a paragraph.</p>
  </div>
);
```

Le JSX est une matière fort complète, il y a encore des choses à connaître mais vous le découvrirez au fur et à mesure de votre apprentissage de React.

Voici néanmoins des liens utiles pour vous aider:

- [Codeacademy :us:](https://www.codecademy.com/learn/react-101)
- [React :fr:](https://fr.reactjs.org/docs/introducing-jsx.html)
- [W3School :us:](https://www.w3schools.com/react/react_jsx.asp)

[:arrow_up: Revenir au top](#reactjs)

### ReactDOM et Render()

```js
import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(
  <h1>Render me!</h1>, document.getElementById('app')
)
```

`ReactDOM` est une librairie JS qui contient des méthodes liés à React. La plus utile pour le moment est `render()`. On va passer en argument notre JSX pour que `render()` l'affiche sur notre page.

`document.getElementById`devrait vous parraître familier. C'est avec lui qu'on indique à l'intérieur de quel élément HTML on veut afficher notre app React. Il suffit de donner à notre `div`une id `app`dans ce cas-ci.

```html
<div id="app">C'est ici que s'affichera notre rendu React</div>
```

Il est possible de passer une variable à `render()`

```js
const myList = {
  js: <li>Julie</li>,
  css: <li>James</li>,
  photo: <li>Chris</li>,
  coms: <li>David</li>,
  boss: <li>Vincent</li>,
};

ReactDOM.render(
myList,
document.getElementById('app')
);
```

[:arrow_up: Revenir au top](#reactjs)

### Import React

Pour pouvoir utiliser React il faut d'abord l'importer dans notre page. Quand on l'importe cela crée un objet qui contient toutes les propriétés dont React à besoin pour fonctionner, y compris pour le JSX et les customs components.

```js
import React from 'react';
```

[:arrow_up: Revenir au top](#reactjs)

### React Components

Les applications React sont faites de plusieurs composants. Mais qu'est-ce qu'un composant?

Il s'agit d'un petit bout de code réutilisable et qui sera en charge d'une seule tâche. Il s'agit souvent de rendre de l'HTML. Vous pouvez créer une infinité de composants pour découper votre app.

Une classe React à besoin d'hériter depuis la classe de base `React.Component` et d'avoir une méthode `render()`. 

```js
class MyComponent extends React.Component {
  render() {
    return <h1>Hello world!</h1>;
  }
}
```

[:arrow_up: Revenir au top](#reactjs)

#### JSX Capitalization

Il est obligatoire que la première lettre de votre composant soit en majuscule. Cela permet à React de faire la distinction entre une balise HTML et un composant.

```js
<MyComponent/>
```

[:arrow_up: Revenir au top](#reactjs)

----

:exclamation: La suite du cours est encore en travaux.

![wip](https://www.avee.no/wp-content/uploads/2018/07/work-in-progress-1.jpg)

### Components Interacting

#### Props

#### Constructor

#### State

### Lifecycle Methods

### Hooks
