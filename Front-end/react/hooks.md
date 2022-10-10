# Hooks

## Route

Le module `react-router-dom` premet de metre en place des route front et de cree une **SPA** (Single Page Application)

### Mise en place du router

La premiere etapes est d'englober l'application dans **BrowserRouter** qui permettra d'utiliser differentes routes

```js
import { createRoot } from "react-dom/client";
import { BrowserRouter } from "react-router-dom";

import Blog from "src/components/Blog";

const target = document.getElementById("root");

const root = createRoot(target);

root.render(
  <BrowserRouter>
    <Blog />
  </BrowserRouter>
);
```

### Gestion des routes

Le composant **Routes** permet de determiner une liste de composant qui seront afficher sur des route

Le composant **Route** permet de decrire l'url et le composant qui sera afficher

Tout les composant a l'exterieur des balises **Routes** seront commun a tout les autre composant

Ici **Header** et **Footer** seront visible sur les routes **Post**, **SingleArticle** et **NotFound**

```js
import { Routes, Route } from "react-router-dom";

import Header from "src/components/Header";
import Posts from "src/components/Posts";
import Footer from "src/components/Footer";
import SingleArticle from "src/components/SingleArticle";
import NotFound from "src/components/NotFound";

function Blog() {
  return (
    <div className="blog">
      <Header />

      <Routes>
        <Route path="/posts" element={<Posts />} />
        <Route path="/article/:slug" element={<SingleArticle />} />
        <Route path="*" element={<NotFound />} />
      </Routes>

      <Footer />
    </div>
  );
}

export default Blog;
```

### NavLink et Link

Le module `react-router-dom` offre les balise **NavLink** et **Link** qui permette de remplacer les balise **a** en evitant de recharger ma page ce qui permet de crée une **SPA**

**NavLink** donne acces a une fonction de className pour gerer si la route est active ou non

```js
import { NavLink } from "react-router-dom";

function Header() {
  return (
    <header className="menu">
      <nav>
        <NavLink
          to="/"
          className={({ isActive }) =>
            isActive ? "menu-link menu-link--selected" : "menu-link"
          }
        >
          {category.label}
        </NavLink>
        <button className="menu-btn" type="button">
          Click
        </button>
      </nav>
    </header>
  );
}

export default Header;
```

### useParams

Ce hook permet de recuperer les parametre des url

```js
import { useParams } from "react-router-dom";

import Post from "../Post";
import NotFound from "../NotFound";

function SingleArticle({ posts }) {
  const params = useParams();

  const foundPost = posts.find((post) => post.slug === params.slug);

  if (!foundPost) {
    return <NotFound />;
  }

  return (
    <div>
      <Post postInfo={foundPost} />
    </div>
  );
}

export default SingleArticle;
```

### useNavigate

Permet de crée une redirection

Ici si on click sur le bouton on sera rediriger sur une nouvelle route sans rechargement

```js
import { useNavigate } from "react-router-dom";

function Posts() {
  const navigate = useNavigate();

  return (
    <main>
      <button type="button" onClick={() => navigate(`/article/toto`)}>
        Click
      </button>
    </main>
  );
}

export default Posts;
```

### useLocation

Permet d'obtenir toutes les information comme l'url sur la quelle l'utilisateur ce situe

Ici a chaque fois que l'utilisateur changera de route le scroll de la page sera ramener en au de page

```js
import { Routes, Route, useLocation } from "react-router-dom";
import { useEffect } from "react";

import Menu from "src/components/Menu";
import Home from "src/components/Home";
import Recipe from "src/components/Recipe";
import Error from "src/components/Error";

function App() {
  const location = useLocation();

  useEffect(() => {
    window.scrollTo(0, 0);
  }, [location.pathname]);

  return (
    <div className="app">
      <Menu />
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/recipe/:slug" element={<Recipe />} />
        <Route path="*" element={<Error />} />
      </Routes>
    </div>
  );
}

export default App;
```
