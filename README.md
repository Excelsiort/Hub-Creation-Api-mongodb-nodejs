# Hub-Creation-Api-mongodb-nodejs
Workshop pour apprendre à créer des apis grace à mongodb et nodejs

Pour commencer nous allons installer nodejs https://nodejs.org/fr/download/ (prendre la derniere version LTS)

Initialiser le projet:

<!--sec data-title="Your first command: OS X and Linux" data-id="OSX_Linux_whoami" data-collapse=true ces-->

    $ npm init -y
    
<!--endsec-->

Puis créer le fichier index.js.

Installer les dépendences suivantes:

<!--sec data-title="Your first command: OS X and Linux" data-id="OSX_Linux_whoami" data-collapse=true ces-->

    $ npm i -s express nodemon
    
<!--endsec-->

Modifier le fichier package.json au niveau du "scripts" (pour lancer le projet avec nodemon et avoir les modifications en direct):

"scripts": { "start": "nodemon index.js"},

Dans index.js se connecter au serveur:

```javascript
const express = require('express');
const app = express();

app.listen(5500 () => console.log('Server started: 5500'));
```
Maintenant que nous pouvons nous connecter au serveur il nous allons créer une base de donnée appelé node-api.

Créer un dossier model contenant dbConfig.js à la racine.

Télécharger MongoDb compass https://www.mongodb.com/try/download/compass

Créer un cluster de type Atlas sur https://account.mongodb.com/account/login?signedOut=true

Se connecter au cluster avec mongoDb Compass grace au lien fourni puis créer une base de donnée

Installer mongoose (package pour utiliser mongodb avec nodejs):

<!--sec data-title="Your first command: OS X and Linux" data-id="OSX_Linux_whoami" data-collapse=true ces-->

    $ npm i -s mongoose
    
<!--endsec-->

Dans mondels/dbConfig.js se connecter à la db:

```javascript
const mongoose = require('mongoose');

mongoose.connect(
  "le lien de connection",
  { useNewUrlParser: true, useUnifiedTopology: true },
  (err) => {
    if (!err) console.log("Mongodb connected");
    else console.log("Connection error :" + err);
  }
)
```

Puis l'appeler dans index.js:

```javascript
require('./models/dbConfig');
```

Créer le fichier postModel.js dans models et créer le model de db pour des posts avec un auteur, un message et une date:

```javascript

   
const mongoose = require("mongoose");

const PostsModel = mongoose.model(
  "node-api",
  {
    author: {
      type: String,
      required: true
    },
    message: {
      type: String,
      required: true
    },
    date: {
      type: Date,
      default: Date.now
    }
  },
  "posts"
);

module.exports = { PostsModel };
```

Créer le dossier routes pour faire le routage de notre api et à l'interieur le fichier postsController.js

Faire une methode Get pour récuperer les données


```javascript
const mongoose = require('mongoose');

mongoose.connect(
  "le lien de connection",
  { useNewUrlParser: true, useUnifiedTopology: true },
  (err) => {
    if (!err) console.log("Mongodb connected");
    else console.log("Connection error :" + err);
  }
)
```

Puis l'appeler dans index.js:

```javascript
require('./models/dbConfig');
```

Créer le fichier postModel.js dans models et créer le model de db pour des posts avec un auteur, un message et une date:

```javascript

const express = require('express');
const router = express.Router();

const { PostsModel } = require('../models/postsModel');

router.get('/', (req, res) => {
  PostsModel.find((err, docs) => {
    if (!err) res.send(docs);
    else console.log("Error to get data : " + err);
  })
});


module.exports = router;

```

Et l'appeler sur index.js: 

```javascript
const postsRoutes = require('./routes/postsController');

```

Pour tester vous pouvez créer un post à la main dans la db:

```json
{
  "author" : "Damien",
  "message" : "on lache r"
}

```
