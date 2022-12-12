# REGEX

Outils sympas pour écrire des regex [ici (regex101)](https://regex101.com/)

La doc [ici (Cheat Sheet)](https://cheatography.com/davechild/cheat-sheets/regular-expressions/)

```js
// Exemple pour vérifier une plaque d'immatriculation française
'/^((?!(SS|WW))[^IOUa-z\d@&"()!_$*€£`+=\/;?#]{2})\-((?!000)\d{3})\-((?!SS)[^IOUa-z\d@&"()!_$*€£`+=\/;?#]{2})$/';

// Pour déclarer une regex
"^ $";

// Pour interdire quelque chose
"(?!k)"; // Interdit la lettre k en minuscule
"(?!(k|L))"; // Interdit la lettre k minuscule ou la lettre L majuscule

// Pour interdire plusieur choses
"[^Abc!§]";

// Pour forcer un caractere
"\-";
"\.";
"\?";

// Pour limiter la chaine de caracteres
"{2,3}"; // Cette chaine de caracteres aura 2 ou 3 carac
"a*"; // Donne rien ou aaaaaaaaaaaaaaaaa
"a+"; // Donne un a ou aaaaaaaaaaaaaaaaa
"a?"; // Donne un a ou rien
"."; // Accepte autant de caracter possible

// Pour regrouper des éléments (organisation)
"((?!b)[a-d]{3})"; // = acd

// Pour regrouper tout les caractères
"[a-z]"; // = a, b, c, ... , z
"[A-Z]"; // = A, B, C, ... , Z
"[0-9]"; // = 0, 1, 2, ... , 9
"\w"; // = [a-zA-Z0-9_]
"\d"; // = [0-9]

// Petits plus
"\s"; // sauter une ligne
"\b"; // fin d'un mots
```

---
