Maintenant nous allons créer les méthodes suivantes:

I. Créer une méthode pour ajouter un post dans la base de donnée avec un auteur et un message
   
   Pour cela installer premierement body-parser pour passer des données à notre application
   
   <!--sec data-title="Your first command: OS X and Linux" data-id="OSX_Linux_whoami" data-collapse=true ces-->

    $ npm i -s body-parser
    
  <!--endsec-->
  
  Utilisez Postman pour tester vos méthodes.
  
  
II. Créer une méthode pour modifier les donnée d'un post déjà existant
     
   Pour cela on utilisera l'_id de l'objet que l'on récupérera avec une méthode de mongoose.
   
III. Créer une méthode pour supprimer un post

Là encore on utilisera l'_id de l'objet
   
IV. Rendre notre Api publique grace à la CORS

