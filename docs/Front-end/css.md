# CSS

Plus d'info [ici (sheets)](https://www.reveillere.fr/M2WEB/sheets/css.pdf) ou [la (CSS CheatSheet)](https://htmlcheatsheet.com/css/)

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
