# Context

A la base de redux

Fait la meme chose mais en moins explicite

Un context a un provider, qui donne acces au valeur defini dans ce context a tout les enfant du provider, qui utiliseront un consumer pour les utiliser

## Dossier context

```js
import { createContext, useState } from "react";

const initialTest = {
  toto: "toto",
  age: 23,
};

export const TestContext = createContext(initialTest);

export const ContextProvider = ({ children }) => {
  const [test, setTest] = useState(initialTest);

  return (
    <TestContext.Provider value={{ test, setTest }}>
      {children}
    </TestContext.Provider>
  );
};
```

## Dans le composant concerner

```js
import { ContextProvider } from ".../testContext";
import SousComposant from ".../sousComposant";

function Test() {
  return (
    <ContextProvider>
      <div>
        <SousComposant />
      </div>
    </ContextProvider>
  );
}
```

## Dans le sous composant consomateur du context

```js
import { TestContext } from ".../testContext";

function SousComposant() {
  return (
    <div>
      <TestContext.Consumer>
        {({ test, setTest }) => {
          <>
            <p>{test.toto}</p>
            <p>{test.age}</p>
            <button
              type="button"
              onclick={() =>
                setTest({
                  ...test,
                  age: test.age + 1,
                })
              }
            >
              + 1
            </button>
          </>;
        }}
      </TestContext.Consumer>
    </div>
  );
}
```

### Ou plus simple

```js
import { useContext } from "react";
import { TestContext } from ".../testContext";

function SousComposant() {
  const testContextValue = useContext(TestContext);

  return (
    <div>
      <p>{testContextValue.toto}</p>
      <p>{testContextValue.age}</p>
      <button
        type="button"
        onclick={() =>
          setTest({
            ...testContextValue,
            age: testContextValue.age + 1,
          })
        }
      >
        + 1
      </button>
    </div>
  );
}
```
