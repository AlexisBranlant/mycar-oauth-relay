# myCar · relais OAuth (GitHub Pages)

Volvo exige une **adresse de retour https publique** (pas de `localhost`). Ces pages statiques, publiées
sur GitHub Pages, servent d'adresse de retour : elles renvoient le navigateur vers votre instance myCar
(locale ou sur la Freebox) avec les paramètres reçus.

- `volvo.html` : adresse de retour à déclarer chez Volvo.
- L'instance cible est lue dans le paramètre `state` (généré par le back myCar).
- Destinations autorisées : réseau local (`localhost`, `192.168.x.x`, `10.x.x.x`, `*.local`…) et les
  origines listées dans `EXTRA_ORIGINS` (ex. votre futur domaine https).
- Aucun secret ici : le code reçu n'est échangeable qu'avec le client secret et le code_verifier PKCE,
  qui restent sur votre serveur.

## Publication

GitHub Pages est gratuit uniquement pour un dépôt **public** : ces fichiers vont dans un dépôt dédié,
séparé du monorepo privé.

1. Créer sur GitHub un dépôt **public et vide** `mycar-oauth-relay`.
2. Y pousser le contenu de ce dossier (à la racine du dépôt).
3. *Settings → Pages* : source « Deploy from a branch », branche `main`, dossier `/ (root)`.
4. L'adresse de retour devient `https://<utilisateur>.github.io/mycar-oauth-relay/volvo.html`.

## Configuration myCar

Dans `.env.local` (ou `.env.prod` sur la Freebox) :

```
VOLVO_REDIRECT_URI=https://<utilisateur>.github.io/mycar-oauth-relay/volvo.html
```

Déclarer exactement la même URL comme *redirect URI* lors de la publication de l'application Volvo.
