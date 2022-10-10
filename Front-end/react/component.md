# Components

## Index root

```js
import { createRoot } from "react-dom/client";
// import du composant principal
import App from "src/components/App";

// on recuperer le composant principal de notre app
// pour cree le DOMvirtuel react
const rootReactElement = <App />;

// on recupere l'element cible dans le fichier html
// pour cree notre racine
const root = createRoot(document.getElementById("root"));

// on ratache les deux pour cree notre rendu react
root.render(rootReactElement);
```

## App (ou composant principal)

App est le composant principal de l'application c'est la que les sous composants sont appeler

Sans utiliser Redux ou d'autre outils qui permette de manipuler le state on passe nos props de notre App au sous composant

```js
import Hello from "./Hello";

function App() {
  const sayHello = "Salut";

  return (
    <div className="app">
      <Hello dirBjr={sayHello} />
    </div>
  );
}

export default App;
```

## Sous composant

Les sous composant recoivent des props depuis leur composant parent et peuvent les utiliser

Par defaut, react nous propose un systeme de typage avec propType mais grace a TypeScrypt on peut ce simplifier le typage de nos props

```js
import PropTypes from "prop-types";

function Hello({ dirBjr }) {
  return (
    <div className="hello">
      <h1>{dirBjr}</h1>
    </div>
  );
}

Hello.propTypes = {
  dirBjr: PropTypes.string.isRequired,
};

export default Hello;
```
