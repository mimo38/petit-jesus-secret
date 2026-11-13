# Petit-Jésus secret

Un tirage au sort de cadeaux (« Secret Santa ») en une seule page web : sans compte, sans serveur, sans publicité, et sans base de données.

**Page en ligne :** <https://mimo38.github.io/petit-jesus-secret/>

## Principe

1. L'organisateur ajoute les participants (prénom, e-mail facultatif), définit si besoin des exclusions, un budget et les modalités de l'échange.
2. Il lance le tirage. Le site ne l'affiche nulle part : il fabrique un **lien personnel** par participant.
3. Chaque lien est envoyé par mail (bouton « Envoyer un mail »). En l'ouvrant, le participant découvre uniquement la personne à qui il offre un cadeau.

L'organisateur ne voit donc pas le tirage, sauf s'il ouvre lui-même les liens.

## Fonctionnalités

- Tirage avec **exclusions** : par exemple deux personnes qui ne doivent pas se tirer, dans les deux sens (couple) ou dans un seul.
- **Budget** et **modalités de l'échange** en texte libre (120 caractères chacun), affichés sur l'écran de résultat.
- **Liste de souhaits** : le bouton « Préparer le fichier liste de souhaits » copie un modèle (un bloc par participant) à coller dans un pad collaboratif comme [Framapad](https://framapad.org/). L'adresse du pad et son mot de passe peuvent être ajoutés aux mails.
- **Texte du mail modifiable**, avec les mots remplacés automatiquement : `{prenom}`, `{evenement}`, `{lien}`, `{liste}`, `{mdp}`.
- **Sauvegarde** : le dernier tirage est gardé dans le navigateur de l'organisateur, et le bouton « Copier tous les liens » permet de le conserver ailleurs.
- Interface en français, adaptée au mobile et au mode sombre.

## Confidentialité : comment ça marche

Le site est un **unique fichier `index.html`**, sans serveur ni compte.

- Le tirage est calculé dans le navigateur de l'organisateur.
- Chaque lien personnel est l'adresse de la page suivie d'un `#` et d'un code. Ce code contient le prénom du participant, le prénom tiré, le nom de l'événement, le budget, l'échange et l'adresse du pad.
- La partie d'une adresse située après le `#` **n'est jamais envoyée au serveur** par le navigateur : GitHub ne voit donc aucun tirage.
- Rien n'est stocké en ligne. Le tirage n'existe que dans les liens.

### Limites à connaître

- **Le code du lien est brouillé, pas chiffré.** C'est suffisant pour un jeu entre proches, mais une personne qui s'y connaît pourrait le décoder. N'y mettez rien de sensible.
- **Quiconque possède un lien connaît sa paire.** Chaque lien doit rester dans le mail de son destinataire.
- **Si les liens sont perdus, le tirage ne peut pas être retrouvé.** L'organisateur doit conserver les mails envoyés ou utiliser « Copier tous les liens ».
- La sauvegarde automatique dépend du navigateur et de l'appareil utilisés pour le tirage.
- Le bouton « Envoyer un mail » repose sur un lien `mailto:` : la longueur du message est limitée par la messagerie. Des champs de texte très longs allongent les liens.
- Le pad de souhaits est accessible à toute personne qui en possède l'adresse. N'y mettez rien de sensible.
- La page charge la police *Bricolage Grotesque* depuis Google Fonts. Pour s'en passer, il suffit de retirer les trois lignes `<link>` correspondantes dans `index.html` : la page utilisera alors une police du système.

## Mise en ligne avec GitHub Pages

1. Créez un dépôt **public** sur GitHub, par exemple `petit-jesus-secret`.
2. Déposez-y le fichier `index.html` (« Add file », puis « Upload files »).
3. Ouvrez « Settings », puis « Pages ». Sous « Build and deployment », choisissez « Deploy from a branch », la branche `main` et le dossier `/ (root)`, puis enregistrez.
4. Au bout de quelques minutes, la page est disponible à l'adresse `https://votre-identifiant.github.io/petit-jesus-secret/`.

### Utiliser votre propre adresse

L'adresse de base des liens personnels est écrite dans `index.html`, dans la fonction qui lance le tirage :

```js
var base = "https://mimo38.github.io/petit-jesus-secret/", ev = $("ev").value.trim();
```

Si vous copiez ce projet sous une autre adresse, remplacez cette valeur par la vôtre. Les liens de l'écran de résultat (« Effectuer mon propre tirage ») pointent aussi vers l'adresse d'origine : modifiez-les de la même manière.

## Utilisation en local

On peut ouvrir `index.html` directement dans un navigateur pour essayer l'interface. Les liens générés pointent toutefois vers l'adresse en ligne : ils ne fonctionnent que si la page y est publiée.

## Structure

```
index.html   La page complète : HTML, CSS et JavaScript, sans dépendance
README.md    Ce fichier
```

## Licence

À définir par le propriétaire du dépôt. Sans licence, le code reste soumis au droit d'auteur par défaut ; vous pouvez en ajouter une depuis GitHub (« Add file », puis « Create new file », puis le nom `LICENSE`).
