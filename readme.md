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