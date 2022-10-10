# TypeScript

`TypeScript` est une version de `javaScript` typé

Les navigateurs ne lisent pas Ts il faut donc compiler ces fichiers pour les transformer en Js

Doc [ici](https://www.typescriptlang.org/docs/)

## TypeScript nécessite une configuration pour être utilisé

Il fait un `package.json` spécifique

```json
{
  "scripts": {
    "build": "tsc", // npm run build pour lancer la compilation
    "start": "node dist/index.js", // npm start pour demarer le server en déploiement
    "dev": "nodemon ./index.ts" // npm run dev nodemon compile ts sans passer par build
  },
  "dependencies": {
    "express": "^4.18.1",
    "typescript": "^4.7.2"
  },
  "devDependencies": {
    "@typescript-eslint/eslint-plugin": "^5.27.0",
    "@typescript-eslint/parser": "^5.27.0",
    "@types/express": "^4.17.13",
    "nodemon": "^2.0.16",
    "ts-node": "^10.8.0"
  }
}
```

Un `.eslint.json` qui lit TypeScript

```json
{
  "env": {
    "browser": true,
    "es6": true,
    "node": true
  },
  "parserOptions": {
    "ecmaVersion": 2020,
    "sourceType": "module"
  },
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint"],
  "extends": ["eslint:recommended", "plugin:@typescript-eslint/recommended"],
  "rules": {
    "@typescript-eslint/indent": ["error", 4],
    "quotes": ["error", "double"],
    "semi": ["error", "always"],
    "no-multi-spaces": "error",
    "no-trailing-spaces": "error"
  }
}
```

Un fichier `tsconfig.json` qui permet la compilation des fichiers ts en js

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "dist", // les fichiers compilés seront mis dans un dossier "dist"
    "sourceMap": true
  },
  "files": [
    "./index.ts", // list des fichier ts à compiler
    "./app/router.ts"
  ],
  "exclude": ["node_modules"]
}
```

Exemple pour un server de base

```js
import * as express from "express";

const app = express();

app.get("/", (req, res) => {
  interface ReceivedMessage {
    content: string;
    pseudo: string;
  }

  async function saveMessage(message: ReceivedMessage) {
    const savedMessage = message;
    console.log("chat", savedMessage.content);
  }

  saveMessage({ content: "to", pseudo: "to" });

  res.send("trop hype");
});

const PORT = process.env.PORT ?? 8000;
app.listen(PORT, () => {
  console.log(`server start on http://localhost:${PORT}`);
});
```

---
