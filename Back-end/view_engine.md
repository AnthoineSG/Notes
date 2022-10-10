# View engine

## Ejs

Ejs est utilisé pour les applications monolithiques, il est simple à utiliser mais pas très ergonomique

La doc [ici](https://ejs.co/#docs)

```html
<!-- Pour afficher une variable -->
<%= nom-varable %>

<!-- Pour afficher un partial ou un component -->
<%- include("path/..ejs") %>

<!-- Boucler sur un tableau -->
<% array.forEach(element => { %> <%= element %> <% }); %>

<!-- Pour accéder a un objet -->
<%= objet.key %>
```

---

## Pug

---
