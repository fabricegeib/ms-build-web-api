# Créer une API web avec Node.js et Express

28 min - [lien](https://learn.microsoft.com/fr-fr/training/modules/build-web-api-nodejs-express/)

## Prérequis
- Git et Node.js installés sur votre ordinateur
- Savoir modifier des fichiers texte et des fichiers de code dans n’importe quel éditeur de texte
- Connaître les bases du protocole HTTP
- Savoir utiliser la ligne de commande, notamment les opérations Git

## Créer une application web de base avec Express

```shell
npm init -y
npm install express
```

Créez un fichier nommé ```app.js``` :

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => res.send('Hello World!'));

app.listen(port, () => console.log(`Example app listening on port ${port}!`));
```

```shell
node app.js
```

Dans un navigateur, accédez à http://localhost:3000

## Créer une application web qui retourne des données au format JSON

Ajoutez le code suivant après ```app.get``` :

```javascript
app.get("/products", (req,res) => {
  const products = [
  {
    id: 1,
    name: "hammer",
  },
  {
    id: 2,
    name: "screwdriver",
  },
  {
    id: 3,
    name: "wrench",
  },
 ];

 res.json(products);
});
```

Dans un navigateur, accédez à http://localhost:3000/products

## Gérer un cycle de vie des requêtes avec un middleware

```javascript
app.use((req, res, next) => {})
```

La méthode passée dans la méthode use() a trois paramètres : req, res, et next. Les paramètres ont la signification suivante :

```req``` : requête entrante qui contient des en-têtes de requête et l’URL appelante. Il peut également contenir un corps de données si le client a envoyé des données avec leur requête.

```res``` : flux de réponse à utiliser pour écrire des informations telles que des en-têtes et des données que vous souhaitez renvoyer au client appelant.

```next``` : paramètre qui signale que la requête est OK et prête à être traitée. Si le paramètre next() n’est pas appelé, le traitement de la requête s’arrête. En outre, il est recommandé d’indiquer au client pourquoi la requête n’est pas traitée, par exemple par un appel à res.send('\<specify a reason why the request is stopped>'\).

## Un pipeline de requête

Si vous avez des itinéraires qui peuvent tirer parti de l’exécution d’un intergiciel ou de la publication d’une requête, configurez-le de sorte que :

- L’intergiciel qui doit s’exécuter avant la requête (pré-requête) est défini avant la demande réelle.
- L’intergiciel qui doit s’exécuter après la requête (post requête) est défini après la demande réelle.

```javascript
app.use((req, res, next) => {
  // Pre request
})
app.get('/protected-resource', () => {
  // Handle the actual request
})
app.use((req, res, next) => {
  // Post request
})

app.get('/login', () => {})
```

Vous pouvez aussi exécuter le code du middleware pré-requête comme argument de la gestion de la requête, comme suit :

```javascript
app.get(
  '/<some route>',
 () => {
   // Pre request middleware
 }, () => {
   // Handle the actual request
 })
```

## Exercice - Gérer le cycle de vie des requêtes

```
git clone https://github.com/MicrosoftDocs/node-essentials

cd node-essentials/nodejs-http/exercise-express-middleware
```

Ce dossier contient trois fichiers : app.js, client.js et package.json.

```shell
npm install
```

Inspectez le code des fichiers ```app.js``` et ```client.js```

### Exécuter le programme Express

Ouvrir deux terminaux distincts puis entrer les commandes suivantes :

```
node app.js

node client.js
```

### Protéger la route
