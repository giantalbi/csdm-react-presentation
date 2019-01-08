# Présentation de Reactjs

## Ce que ce n’est pas ?
Une librairie de style (ex: Bootstrap, materialize-css, etc)

## Ce que c’est ?
Une libraire pour construire des interface dynamique en JS / ES6

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


# Prérequis

## Installation de Node

### Windows 
TODO

### Linux / WSL
1. Installer NPM
```
sudo apt install npm
```
2. Installer "n" de façon globale:
```
sudo npm install -g n
```
3. Installer la dernière version de Node avec n: 
```
n latest
```

## Utilitaire create-react-app
Permet de créer un projet react rapidement sans avoir à configurer les packages nécessaire pour le bundling comme **Webpack** ou de configurer le transpillage de ESCMAScript 6 vers la version supporté de Node avec **babel**

Il suffit d'installer le package NPM globale 
```
sudo npm install -g create-react-app
```


# Aller plus loins
## Redux
Librairie Javascript permettant une gestion d’état (state) par conteneur
Permet une gestion plus “clean” des données d’une application grace à un flow de donnée de type flux.
### Concepts de bases
https://redux.js.org/introduction/coreconcepts
Tous les états (states) sont stocké dans un conteneur (store)
