# node-allocine-api

Module Node.js permettant d'accéder à l'API d'Allociné.

Aucune dépendance nécessaire ! Il utilise uniquement des modules du core.

Il s'agit de l'un de mes premiers modules Node.js, donc soyez indulgents et n'hésitez pas à me suggerer des améliorations !

## Installation

Pour l'installer, ajoutez simplement ce dépôt aux dépendances de votre fichier package.json :

```json
"dependencies" : {
	...
    "allocine-api": "https://github.com/leeroybrun/node-allocine-api/tarball/master"
}
```

Appelez ensuite simplement `npm install`, et npm installera le module pour vous.

## Utilisation

Pour l'utiliser, incluez-le simplement dans les fichiers de votre application :

```javascript
var allocine = require('allocine-api');
```

### API

Pour l'instant ce module ne comprend qu'une seule méthode pour accéder à l'API. Celle-ci est plus que suffisante puisqu'elle vous permet d'appeler l'API comme bon vous semble. D'autres méthodes feront peut-être leur apparition plus tard afin de faciliter l'accès à l'API.

Pour plus d'informations sur l'API Allociné, je vous invite à vous rendre sur le wiki de Gromez : http://wiki.gromez.fr/dev/api/allocine_v3

#### allocine.api(method, options, callback)

Cette fonction va appelé l'API définie (`method`) en lui fournissant les `options` (objet) passées en paramètre, puis appelera la fonction de `callback` en lui fournissant le résultat sous forme d'objet.

Exemples :
```javascript
// Recherche de tous les films spiderman
allocine.api('search', {q: 'spiderman', count: 20, filter: 'movie'}, function(results) { console.log(results.feed.totalResults); });

// Informations sur un film particulier
allocine.api('movie', {code: 128188}, function(result) { console.log(result.movie.title); });
```

**Attention !** Il semble que si vous essayiez de modifier l'option `filter`, par exemple pour ne récupérer que les films, vous devez alors définir l'option `count`. Sinon, l'API refusera votre appel et retournera une erreur 403. C'est très bizarre, mais il s'agit peut-être là d'une limitation ou d'une mesure de sécurité mise en place par Allociné.