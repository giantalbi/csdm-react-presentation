# Présentation de Reactjs

## Ce que ce n’est pas ?
Une librairie de style (ex: Bootstrap, materialize-css, etc)

## Ce que c’est ?
Une libraire pour construire des interface dynamique en JS / ES6 à l'aide de JSX

### Exemple d'un composant React
```javascript
import React, {Component} from 'react';

class Home extends Component{
    state = {
        foo: "bar"
    }

    constructor(props){
        super(props);
    }

    render(){
        return(
            <div>
                <h2>My react hommepage</h2>
                <h3>{ this.state.foo }</h3>
            </div>
        );
    }
}
```

## Points négatifs (Opinion personnelle)
* DEPENDENCY HELL!!!
* Nécessité de beaucoup de librairies supplémentaires pour une expérience complète
* Courbe d’apprentissage
* Confusions entre Props et States et leurs cas d’utilisations

## Points positifs 
* Free Open Source: License MIT :
Si un bug est dans la librairie, il est possible de le corriger sois même et de faire un Pull Request sur le repo de React pour le corriger
* Compatible ECMAScript 6 +
* Beaucoup de librairies pour facilité le développement
    * React-router: Routage des vues
    * Axios: Meilleur librairie de requêtes
    * React-Redux: (Voir Redux)
    * React-Thunk: Meilleur gestion des actions de Redux

# Avantages de ES6 par rapport à ES5 et antérieur

## Arrow functions
```javascript
function doSomething(callback){
    callback("First", "Last");
}


// ES6
doSomething((param1, param2) => {
    console.log("Something");
});

// ES5
doSomething(function(param1, param2){
    console.log("Something")
})
```

## Paramètres par défaut
```javascript
function foo(x = 1){
    console.log(x);
}

foo()
// > 1

foo(42)
// > 42

```
## Rest parameters
Accumulation des paramêtres supplémentaires dans une seul variable
```javascript
function foo(x, y, ...param){
    console.log(param);
}

foo(1, 2);
// > Array[]

foo(1, 2, "bar", 1, {a: "b"})
// > Array["bar", 1, {a: "b"}]
```

## Spread operator
Dérouler les valeurs d'un tableau à l'aide de l'opérateur `...varialbe`
```javascript
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
arr1.push(...arr2);

console.log(arr1);
// [0, 1, 2, 3, 4, 5]
```

## Syntaxe pour propriété
Permet d'addresser une propriété plus rapidement
```javascript
let x = 3;
function foo(obj){
    console.log(obj.x)
}

// ES6
foo({ x })

// ES5
foo({ x: x })

```

## Assignement destructeur
Permet d'aller chercher une valeur dans un object plus facilement
```javascript
function foo(){
    return {
        bar: "42",
        x: 0,
        y: 4
    }
}

// ES6
const { bar, y } = foo();

console.log(bar) // "42"
console.log(y) // 4

// ES5
const bar = foo().bar;
const y = foo().y;

console.log(bar) // "42"
console.log(y) // 4
```


## Et tellement de belles améliorations qui rendent le javascript plaisant à utiliser
* De vraies **classes** OOP (et non des prototypes)
* **Foreach** `for(let i in arr)`
* **Promise** pour meilleur programmation orientée évènements

Pour plus d'exemples voir http://es6-features.org/

# Concept fondamentaux de React
> Basé sur la documentation officielle ainsi que mon expérience  personnelle

Tout ce que React fait ce réduit à un élément HTML racine
```html
<!--index.html-->
<!DOCTYPE html>
<html>
    <head>
        <title>React test</title>
    </head>
    <body>
        <div id="root"></div>
    </body>
</html>
```

ainsi que l'initialization du ReactDOM sur cet élément racine
avec un élément JSX
```javascript
// index.js
import ReactDOM from 'react-dom';

ReactDOM.render(<h1>This is a valid react app</h1>, document.getElementById('root'))
```
Il est ensuite possible d'avoir des élément JSX plus "complèxes" avec l'utilisation de composante

## **J**avascript **S**yntax e**X**tension
JSX est une extension de la syntaxe javascript permettant de
d'avoir une description plus explicite de notre interface
tout en mixant du javascript régulié

```javascript
const utilisateur = {
    nom: "Allen",
    prenom: "Samuel"
};
const element = (<h2>Bonjour { utilisateur.prenom }</h2>);
```

## Composante React
Un composante React n'est qu'une classe retournant du JSX pouvant être rendu par le ReactDOM.

```javascript
// card.js
import React, { Component } from 'react';

class Card extends Component{
    render(){
        return (
            <div>
                Ceci est une carte
            </div>
        );
    }
}
```
```javascript
// index.js
import Card from './Card';
import ReactDOM from 'react-dom';

ReactDOM.render(<Card/>, document.getElementById("root"));
```

## États (states) et propriétées (props)
L'avantage des composantes est qu'il peuvent gèrer différent
type de donnée.

### Les propriétés
Les propriétés sont une type de donnée immutable pouvant être transmis avec des attributs JSX pouvant être utilisé par la composante.

```javascript
// index.js
import ReactDOM from 'react-dom';
import React, {Component} from 'react';

class Salutation extends Component{
    constructor(props){
        // Il est important de toujours passer le props à la classe de base
        super(props)
    }


    render(){
        return(
            <h1>Bonjour {this.props.prenom}</h1>
        )
    }
}

const foo = "Samuel";

ReactDOM.render(<salutation prenom={ foo } />, document.getElementById("root"));

```
Les propriétés sont en lecture-seul, comme les props servent d'entrée pour notre composante elle ne doivent donc pas être modifié, cela pourrais compromettre la pureté de notre composante

Pour citer la documentation officielle de React:
>React is pretty flexible but it has a single strict rule:

>All React components must act like pure functions with respect to their props.

### Les états
Contrairement aux propriétés, les états servent à gèrer les données d'une composante à l'interne et permettent des comportements dynamiques. Les états on la possibilité de modifier le ReactDOM à l'aide de la méthode `setState()` indiquant au react DOM de re-appeller la méthode `render()` de notre composante.

```javascript
// index.js
import ReactDOM from 'react-dom';
import React, {Component} from 'react';

class foo extends Component{
    state = {
        valeur: 0
    }

    constructor(props){
        super(props)

        /*
        Ici il est correcte de modifier directement le state
        car le React DOM n'a pas encore appeller le render()
        */
       this.state.random = Math.floor(Math.random()*10);
    }

    componentWillMount(){
        
    }

    componentDidMount(){
        this.timer = setInterval(() => {

            // Modifier directement une valeur du state
            this.setState({ random: Math.floor(Math.random()*10) })

            /*
            Modifier le state par rapport à la précédente valeur de notre state
            */

            // Correcte
            this.setState((prevState, props) => ({
                valeur: prevState.valeur + 1
            }));

            /*            
            Comme notre state peut être modifier de façcon 
            asynchrone, il est important dans ce cas si de le 
            modifier avec la précédente signature de setState
            car celle si ne fait pas référence au précédente état du state mais l'état actuel
            */
            // Incorrecte, mais techniquement faisable
            this.setState({
                valeur: this.state.valeur + 1
            })
        }, 1000);
    }

    componentWillUnmount(){
        clearInterval(this.timer);
    }    

    render(){
        return(
            <h1>La valeur est {this.state.valeur} et la valeur aléatoire est {this.state.random}</h1>
        )
    }
}

ReactDOM.render(<salutation prenom={ foo } />, document.getElementById("root"));
```

Quoi retenir pour correctement utiliser les états:
* `setState(obj)` pour déclencer une mise à jours du ReactDOM
* `setState((prevState, props) => {})` pour mettre à jours du DOM à partir du précédent état
* `componentDidMount()` est appellée après que notre composante sois insèré dans le DOM
    * Il est impportant de mettre les requêtes de donnés dans cette méthode et non dans le constructeur car la mise à jours du DOM sera retardé
* `componentWillUnmount()` est appellée après que la composante 
sois retiré du DOM (agis comme un **destructeur**)
* `componentDidUpdate()` est appellée à chaque fois que le ReactDOM met à jour la composante

## Rendu conditionnel
### Utilisation de l'opérateur **&&**
```javascript
// card.js
import React, { Component } from 'react';

class Card extends Component{
    render(){
        const { type } = this.props;
        return (
            <div>
                {type == "danger" &&
                    <b>Attention</b>
                }
                Ceci est une carte
            </div>
        );
    }
}
```

### Utilisation du if ternaire
```javascript
// card.js
import React, { Component } from 'react';

class Card extends Component{
    render(){
        const { type } = this.props;
        return (
            <div>
                <b>{type == "danger" ? "Attention": "Info"}</b>
                Ceci est une carte
            </div>
        );
    }
}
```


# Prérequis
## Installation de Node

### Windows 
TODO

### Linux / WSL
1. Installer NPM
```
$ sudo apt install npm
```
2. Installer "n" de façon globale:
```
$ sudo npm install -g n
```
3. Installer la dernière version de Node avec n: 
```
$ n latest
```

## Utilitaire create-react-app
Permet de créer un projet react rapidement sans avoir à configurer les packages nécessaire pour le bundling comme **Webpack** ou de configurer le transpillage de ESCMAScript 6 vers la version supporté de Node avec **babel**

Il suffit d'installer le package NPM globale 
```
$ sudo npm install -g create-react-app
```


# Aller plus loins
## Test unitaire avec Jest
Jest est le framework de test de facebook, React étant aussi par Facebook, il est logique d'utiliser leur framework.

Il viens préinstaller avec notre package create-react-app

Il ne suffit que de tapper
```
$ npm test
```
et notre menu de test apparaitra

## Redux
Librairie Javascript permettant une gestion d’état (state) par conteneur
Permet une gestion plus “clean” des données d’une application grace à un flow de donnée de type flux.
### Concepts de bases
https://redux.js.org/introduction/coreconcepts
Tous les états (states) sont stocké dans un conteneur (store)

## React-Native

