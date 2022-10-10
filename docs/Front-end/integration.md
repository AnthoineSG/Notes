# Front

## HTML

Plus d'info [ici](https://htmlcheatsheet.com/)

```html
<!DOCTYPE html>
<html lang="fr">
  <head>
    <title>TITRE DANS L'ONGLET</title>
    <link rel="stylesheet" href="style.css" />
    <script src="main.js"></script>
  </head>

  <body>
    <header>
      <h1>TITRE</h1>
      <h2>SOUS-TITRE</h2>
    </header>

    <main>
      <article>
        <section>
          <p id="" class="">TEXT</p>
          <a href="#">LIENS</a>
          <ul>
            <li>LISTE</li>
          </ul>
          <br />
          <strong>BOLD</strong>
          <em>ITALIC</em>
          <img src="#" alt="description" />

          <iframe src="#" width="200" height="200">TRUC A IMPRIMER</iframe>

          <form action="/" method="post">
            <fieldset>
              <legend>NOM DU FORMULAIRE</legend>
              <label for="">NOM DU CHAMPS</label>
              <input type="text" id="" value="" />
              <select name="">
                <option value="">LISTE DEROULANTE</option>
              </select>
            </fieldset>
            <textarea cols="20" name="" rows="5">ZONE DE TEXT</textarea>
            <button type="submit">VALIDATION DU FORMULAIRE</button>
          </form>
        </section>
      </article>
    </main>

    <footer>
      <div>PAS DE VALEUR CONTEXTUEL</div>
      <span>PAS DE VALEUR CONTEXTUEL</span>
    </footer>
  </body>
</html>
```

---

## CSS

Plus d'info [ici](https://www.reveillere.fr/M2WEB/sheets/css.pdf) ou [la](https://htmlcheatsheet.com/css/)

```css
/* Selectionner une balise */
body {
  --color-red: red;

  display: flex;
  flex-flow: column wrap;
  align-items: center;
  justify-content: space-around;
}

/* Selection par une class */
.class {
  width: 1vw;
  height: 1vh;
  font-size: 1rem;
}

/* Selection par un id */
#id {
  color: var(--color-red);
}

/* Selection d'un input avec une valeur precise */
input[value="toto"] {
  background-color: antiquewhite;
}
```

---

## JS vanilla

La bible c'est la [MDN](https://developer.mozilla.org/fr/)

```js
// Les variable
const toto = true;
let tata = 10;
tata = "string";

// Les fonction
async function faiDesTruc(toto) {
  const attend = await truc;
  return attend;
}
faiDesTruc(toto);

// Les array
const tableau = [1, 2, 3, 4, 5, 6];

for (const nbr of tableau) {
  console.log(nbr);
}

tableau.forEach((nbr) => {
  console.log(nbr);
});

const trouver = tableau.find((nbr) => (nbr = 4)); // 4

const pourChaque = tableau.map((nbr) => nbr / 3); // [3, 6, 9, ...]

const filtre = tableau.filter((nbr) => nbr <= 2); // [1, 2]

tableau.sort(); // range le tableau par ordre alphabétique ou numerique

// Les objet
const obj = {
  key: "value",
  fonction(params) {
    return params;
  },
};
console.log(obj.fonction(toto));
```

---
