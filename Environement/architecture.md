# Architecture

Exemple pour une application bien structurée

```bash
.
├── README.md
├── .gitignore
├── .eslintrc
├── client
│   ├── package.json
│   ├── README.md
│   ├── docs
│   └── public
│      ├── images
│      └── src
│           ├── css
│           │   ├── reset.css
│           │   └── styles.css
│           ├── html
│           │   └── home.html
│           └── js
│               └── main.js
└── server
    ├── package.json
    ├── .env
    ├── .env.exemple
    ├── data
    │   ├── MCD.md
    │   ├── MLD.md
    │   ├── MPD.md
    │   ├── tables.sql
    │   ├── data.sql
    │   └── sqitch
    ├── docs
    ├── logs
    │   └── 2022-logs.txt
    └── api
        ├── tests
        ├── public
        │   ├── css
        │   ├── html
        │   └── js
        ├── index.js
        └── app
            ├── controllers
            │   └── index.js
            ├── services
            │   └── index.js
            ├── models
            │   ├── index.js
            │   └── config
            │       └── dbconnect.js
            ├── middleware
            │   ├── errors
            │   │   ├── 404.js
            │   │   └── 500.js
            │   ├── helpers
            │   │   └── loggers.js
            │   ├── validation
            │   │   └── schemas
            │   └── errorHandling.js
            └── route
                └── index.js
```

Exemple pour une application monolithique

```bash
.
├── package.json
├── .env
├── .env.exemple
├── .eslintrc
├── data
│   ├── MCD.md
│   ├── MLD.md
│   ├── MPD.md
│   ├── tables.sql
│   ├── data.sql
│   └── sqitch
├── docs
├── logs
├── tests
├── index.js
└── app
    ├── controllers
    │   └── index.js
    ├── models
    │   ├── index.js
    │   └── config
    │       └── dbconnect.js
    ├── views
    │   ├── components
    │   │   └── nav.ejs
    │   ├── errors
    │   │   └── 404.pug
    │   ├── partial
    │   │   └── header.pug
    │   └── index.html
    ├── middleware
    │   ├── errors
    │   │   ├── 404.js
    │   │   └── 500.js
    │   ├── helpers
    │   │   └── loggers.js
    │   ├── validation
    │   │   └── schemas
    │   └── errorHandling.js
    └── route
        └── index.js
```

---
