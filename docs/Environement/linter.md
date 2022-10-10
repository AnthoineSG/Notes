# Linter

## Eslint

Eslint permet d'analyser le code écrit et de corriger les potentielles erreurs de syntaxe

Doc [ici](https://eslint.org/demo)

Pour l'installer en global sur sa machine

```bash
npm i -g eslint
```

Installer l'extension vscode eslint

Pour un fichier config de base

```json
{
  "extends": "eslint:recommended",

  "parserOptions": {
    "ecmaVersion": 2020,
    "sourceType": "module"
  },

  "env": {
    "browser": true,
    "es6": true,
    "node": true
  },

  "rules": {
    "indent": ["error", 4],
    "quotes": ["error", "double"],
    "semi": ["error", "always"],
    "camelcase": "error",
    "no-var": "error",
    "no-multi-spaces": "error",
    "no-trailing-spaces": "error"
  }
}
```

---

## TsLint

---
