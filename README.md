![Preview](./design/desktop-preview.jpg)

## Le challenge

Votre challenge est de créer une application de tracking d'IP sur base des previews fournies.
Afin de trouver la localisation des adresses IP, vous utiliserez l'[API de géolocalisation d'IP par IPify](https://geo.ipify.org/). Pour générer la carte, [LeafletJS](https://leafletjs.com/) est recommandé.

L'utilisateur devrait pouvoir :

- Voir leur propre adresse IP sur la carte au chargement de la page
- Chercher n'importe quelle adresse IP ou domaine et en voir les informations clef et la localisation sur la carte

---

⚠️ **IMPORTANT** ⚠️: Pour utiliser l'API de géolocalisation d'IP d'IPify, vous devrez vous inscrire avec un compte gratuit. Vous n'avez pas besoin d'entrer des données de carte banquaire et c'est un processus rapide. Cela générera une API key 🔑 rien que pour vous (qu'ils sont gentils). Généralement, vous devriez pouvoir restreindre cette clef à une url spécifique (votre propre domaine) afin d'empêcher d'autres personnes d'utiliser votre clef pour leur sites. IPify n'a pas cette fonction car vous n'ajoutez pas vos données de carte banquaire, ce n'est pas un problème. **Par conséquent, soyez sûr de bien vous inscrire pour un compte gratuit _uniquement_ et de NE PAS entrer de données de carte de banque**

Pour l'API de carte, [LeafletJS](https://leafletjs.com/) est recommandée. C'est gratuit et ne nécessite pas de clef API. Vous êtes libres d'utiliser d'autres API comme Google Map ou Mapbox.

Voici des guides si vous décidez d'utiliser l'une de ces deux dernières :
- [API Key best practices from Google Developers](https://developers.google.com/maps/api-key-best-practices)
- [How to use Mapbox securely](https://docs.mapbox.com/help/troubleshooting/how-to-use-mapbox-securely/)

Exposer votre clef API publiquement peut avoir comme conséquence que d'autres personnes l'utiliseront pour leur propre application si vous ne prenez pas vos précautions. Lisez bien les guides et suivez les recommandations.

**Bon courage!** 👾