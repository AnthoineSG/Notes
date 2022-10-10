# Redux

Redux est un module de gestion du state de react

Il permet de mettre le state dans un store et le rend disponible dans tout les composant de l'application ce qui permet deviter de devoir passer tout nos etat par des props et de favoriser le SOC

Avec redux classique on a acces a 3 methodes

- `store.getState()` : pour recuperer notre state dans notre application
- `store.dispatch({ ... })` : pour effectuer une action
- `store.subscribe(() => { ... })` : pour effectuer un rendu a chaque fois qu'une valeur du state change

![Redux](/assets/images/redux/Redux.png)

---

Le module `react-redux` offre des hooks simplifier pour effecter la gestion du state

- useSelector((state) => state.TRUC) : qui permet d'acceder directement a une valeur de notre state
- useDispatch({ ... }) : qui permet d'effectuer une action

A chaque mise a jour du state, `react-redux` effectue un nouveau rendu

![Redux](/assets/images/redux/Redux_communication.png)

## Mise en place de redux

### Index de l'application react

Comme pour le module router-react-dom on englobe notre application react dans un Provider et on lui donne le store avec en paramettre

```js
import { BrowserRouter } from "react-router-dom";
import { createRoot } from "react-dom/client";
import { Provider } from "react-redux";

import App from "src/components/App";
import store from "src/store";

const rootReactElement = (
  <Provider store={store}>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </Provider>
);

const root = createRoot(document.getElementById("root"));
root.render(rootReactElement);
```

### Index du store

Pour crée un store avec redux plusieurs elements sont necessaire

- un state initial : qui determine notre state de base avant modification
- des actions : qui permet de dire ce que l'on veux faire
- un reducer : qui traduit nos actions et les interprete
- des middlewares : qui permet defectuer des fonction asynchrone

Ici on crée notre store avec la fonction createStore et on lui donne en argument notre reducer et nos middlewares

```js
import { createStore, applyMiddleware, compose } from "redux";

import reducer from "src/store/reducers";
import dataMiddleware from "./middlewares/dataMiddleware";
import recipesMiddleware from "./middlewares/recipesMiddleware";

const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;

const enhancers = composeEnhancers(
  applyMiddleware(dataMiddleware, recipesMiddleware)
);

const store = createStore(reducer, enhancers);

export default store;
```

## Reducer

Ici si notre action est de type `GET_DATA` on retournera un nouveau state avec la key **isLoading** qui aura changer

- `initialState` est le state par defaut au lancement de notre application

```js
import { GET_DATA } from "../actions/recipes";

export const initialState = {
  list: [],
  isLoading: true,
  favorites: [],
};

const reducer = (state = initialState, action = {}) => {
  switch (action.type) {
    case GET_DATA:
      return {
        // on copie tout le state actuel
        ...state,
        // on change la valeur qui nous interesse
        isLoading: true, // ou action.isLoading par exemple
      };

    default:
      return state;
  }
};

export default reducer;
```

### combineReducers

On peut utiliser `combineReducers` pour combiner plusieurs reducer

Les valeurs du state seront aussi separer :

- Pour recuperer des valeur du state de recipes `state.recipe.list`
- Pour recuperer des valeur du state de user `state.user.email`

```js
import { combineReducers } from "redux";

import recipesReducer from "./recipes";
import userReducer from "./user";

const rootReducer = combineReducers({
  recipes: recipesReducer,
  user: userReducer,
});

export default rootReducer;
```

## Actions

Permet de mieux s'organier en utilisant des constantes et des fonction plutot que des string et des objet

```js
export const GET_DATA = "GET_DATA";

export const getData = () => ({
  type: GET_DATA,
});
```

### Exemple

A chaque nouveau rendu on recupere toutes les données

```js
import { useEffect } from "react";
import { getData } from "src/store/actions/recipes";

import Menu from "src/components/Menu";

function App() {
  useEffect(() => {
    dispatch(getData());
  }, []);

  return (
    <div className="app">
      <Menu />
    </div>
  );
}

export default App;
```

## Middlewares

Permet de realiser des fonction asynchrone comme par exemple des requete a une API

Il aggisent comme des videurs chaqu'un a la suite des autres.

```js
// ...
import dataMiddleware from "./middlewares/dataMiddleware";
import recipesMiddleware from "./middlewares/recipesMiddleware";
// ...
const enhancers = composeEnhancers(
  applyMiddleware(
    dataMiddleware, // 1er middleware a agir
    recipesMiddleware // 2nd a agir il aura acces au state mis a jour par le 1er
    // etcetc autant de Mw que l'on veux
  )
);

const store = createStore(reducer, enhancers);

export default store;
```

![Redux](/assets/images/redux/Redux_Mw_principe.png)

---

A chaque rendu de l'application les Mw seront traverser

Si une action est capter dans un Mw une action sera effectuer et une nouvelle action sera créé a la suite

![Redux](/assets/images/redux/React-Redux_Principe_middleware.png)

![Redux](/assets/images/redux/Redux_Mw_discution.png)

---

### Utilisation

Les middleware utilise `redux` et pas `react-redux` on ne peut donc pas utiliser les hooks useSelector et useDispatch mais les methode du store de redux

A chaque fin d'action on next pour que le state evolue et ne reste pas figer

```js
import axios from "axios";

import { GET_DATA, getDataSuccess } from "../actions/recipes";

const dataMiddleware = (store) => (next) => (action) => {
  switch (action.type) {
    case GET_DATA: {
      axios("http://localhost:8080/recipes")
        .then((res) => {
          store.dispatch(getDataSuccess(res.data));
        })
        .catch((error) => {
          console.log(error);
        });
      next(action);
      break;
    }

    default:
      next(action);
      break;
  }
};

// equivalent

// const dataMiddleware = (store) => {
//   return (next) => {
//     return (action) => {
//       // fait des truc
//     }
//   }
// }

export default dataMiddleware;
```
