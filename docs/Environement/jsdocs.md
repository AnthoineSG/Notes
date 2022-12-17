# JSDoc

Natif à js permet de commanter ses fonctions, methodes, const, ...

Doc [ici](https://jsdoc.app/)

```js
/**
 * Fonction qui fait rien de special
 * @param {*} req récupere les paramètres dans l'url et l'affiche dans le terminal
 * @param {*} res renvoie un simple "hello"
 */
function toto(req, res) {
  /**
   * Recupere les parametres "/?name=..."
   */
  const params = req.params.name;
  console.log(params);
  res.send("hello");
}
```

---
