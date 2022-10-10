# State

## State React

Pour manipuler le state avec react on peut utiliser la methode useState

Cette methode nous renvoie un tableau avec :

- une variable comportant le state
  - ici **isClicked** vaux false et ne peut pas etre modifier
- une fonction de modification du state
  - ici **setIsClicked** permet de modifier la valeur de isClicked pour la passer a true

```js
function toto() {
  const [isClicked, setIsClicked] = useState(false);

  const handleShowMessage = () => {
    setIsClicked(true);
  };

  const handleHiddenMessage = () => {
    setIsClicked(false);
  };

  return (
    <div>
      <h1>Bienvenue</h1>

      {isClicked && <p>toto</p>}

      <button type="button" onClick={handleShowMessage}>
        Click pour afficher le message
      </button>

      <button type="button" onClick={handleHiddenMessage}>
        Click pour retirer le message
      </button>
    </div>
  );
}

export default toto;
```
