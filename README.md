# Alive

Un petit zombie kawaii et pataud, en pyjama raccommodé, se fraie un chemin parmi les Terreurs d'un monde d'horreur pour retrouver les reliques de son enfance et les rapporter dans sa cabane.

Cette version est une **PWA** (application web installable) : elle s'installe sur l'écran d'accueil d'un téléphone ou sur un ordinateur, s'ouvre en plein écran et reste jouable hors ligne.

## Documents

- [Conception et feuille de route](docs/alive-conception.md) : pitch, personnages, L'Aveugle, cabane et reliques, bruit, faim, prochaines étapes.
- [Animations](docs/alive-animations.md) : principes communs, marche, états et chiffres du petit zombie et de L'Aveugle.

## Contenu

| Fichier | Rôle |
|---|---|
| `index.html` | Le jeu (prototype « L'Aveugle » : le petit zombie, sa cabane-refuge, les reliques et la première Terreur) |
| `manifest.webmanifest` | Nom, icônes, couleurs et captures de l'application installée |
| `sw.js` | Service worker : met le jeu en cache pour jouer hors ligne |
| `icons/` | Icônes de l'application (192, 512, version « maskable », icône Apple, favicon) |
| `screenshots/` | Captures affichées par la fenêtre d'installation (ordinateur et téléphone) |
| `docs/` | Documents de conception et d'animation |

## Jouer

- **ZQSD** ou **flèches** : marcher (peu de bruit). **Maj** : courir (très bruyant).
- **F** : faire le mort (encore F ou bouger pour se relever). **G** : grogner. **E** : manger.
- Ramasse une relique en marchant dessus, puis rapporte-la dans la cabane : arrête-toi devant l'ouverture pour t'y glisser, recule pour sortir.
- Sur téléphone : glisse le doigt pour marcher (plus loin pour courir), boutons « Mort » et « Sauter ».
- Clique dans le décor si le clavier ne répond pas.

## Jouer sur l'ordinateur

Pas besoin de serveur : double-clique sur `index.html`, le jeu s'ouvre dans le navigateur.

L'installation (icône sur l'écran d'accueil, plein écran) et le jeu hors ligne passent par la version en ligne sur GitHub Pages : un navigateur ne les active pas pour un fichier ouvert directement.

## Publier avec GitHub Pages

1. Pousse ce dossier sur GitHub (dépôt `alive`).
2. Dans le dépôt : **Settings → Pages → Build and deployment**, source **Deploy from a branch**, branche `main`, dossier `/ (root)`.
3. Le jeu sera en ligne sur `https://<ton-compte>.github.io/alive/`. Tous les chemins sont relatifs, il fonctionne dans ce sous-dossier.

## Installer sur un téléphone

- **Android (Chrome)** : ouvre l'adresse, puis « Installer l'application » (ou menu ⋮ → « Ajouter à l'écran d'accueil »).
- **iPhone / iPad (Safari)** : bouton Partager → « Sur l'écran d'accueil ».

## Publier une nouvelle version

1. Remplace `index.html` par la nouvelle version du jeu.
2. Dans `sw.js`, change `VERSION` (par exemple `alive-v0.1.1`) : l'ancien cache est supprimé et les joueurs reçoivent la nouvelle version au lancement suivant.
