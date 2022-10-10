# Securiter

Ref obligatoire a connaitre [OWASP](https://owasp.org/www-project-top-ten/)

## Failles XSS

Les failles XSS on pour principe de placer du code malveilant dans des formulaires qui seront sauvegerder en base de données et qui auront un impact sur l'experience des autre utilisateurs

Pour sens prevenir il faut mettre en place des verification des formulaire en front comme en back (et meme en BDD) de nombreux module existe pour renforcer le filtrage des formulaire mais une simple echapement des caractere avant de les stocker en base de données suffie pour eviter d'introduire des balise HTML ou des scripts

![XSS principe](/assets/images/securiter/schema_faille_XSS.png)

![XSS comment](/assets/images/securiter/schema_faille_XSS-2.png)

---

## Injection SQL

Injection de code SQL a travers les requete en base de données

Elles peuvent mener a des modification voir a la suppression de données en BDD

Pour les eviter utiliser des requetes parametrer en back et verifier tout ce qui transite entre `front <-> back <-> BDD` comme les formulaire et les paramettre des requete

---

## Attaques CSRF

Ajout d'element malveiant sur l'application comme par exemple un popup avec marquer "cliquer ici" et qui va voler les information de connexion de l'utilisateur

Pour eviter ses attaques mettre en place des cookie secret avec JWT par exemple

![modification pour ce faire passer pour quelqu'un d'autre](/assets/images/securiter/JWT_signature.png)

---

## Man in the middle

Utilisateur non voulu qui requete une API

A et B parlent et C tape une incruste et parle a B

Pour eviter ses attaques mettre en place des cors sur le serveur pour autoriser seulement certain nom de domaine a requeter l'API

![cros origin](/assets/images/securiter/cors_origin.png)

---
