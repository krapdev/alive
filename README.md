# Alive

Un petit zombie kawaii et pataud, en pyjama raccommodé, se fraie un chemin parmi les Terreurs d'un monde d'horreur pour retrouver les reliques de son enfance et les rapporter dans sa cabane.

Cette version est une **PWA** (application web installable) : elle s'installe sur l'écran d'accueil d'un téléphone ou sur un ordinateur, s'ouvre en plein écran et reste jouable hors ligne.

## Contenu

| Fichier | Rôle |
|---|---|
| `index.html` | Le jeu (prototype « L'Aveugle » : le petit zombie, sa cabane-refuge, les reliques et la première Terreur) |
| `manifest.webmanifest` | Nom, icônes, couleurs et captures de l'application installée |
| `sw.js` | Service worker : met le jeu en cache pour jouer hors ligne |
| `icons/` | Icônes de l'application (192, 512, version « maskable », icône Apple, favicon) |
| `screenshots/` | Captures affichées par la fenêtre d'installation (ordinateur et téléphone) |

## Jouer

- **ZQSD** ou **flèches** : marcher (peu de bruit). **Maj** : courir (très bruyant).
- **F** : faire le mort (encore F ou bouger pour se relever). **G** : grogner. **E** : manger.
- Ramasse une relique en marchant dessus, puis rapporte-la dans la cabane : arrête-toi devant l'ouverture pour t'y glisser, recule pour sortir.
- Sur téléphone : glisse le doigt pour marcher (plus loin pour courir), boutons « Mort » et « Sauter ».
- Clique dans le décor si le clavier ne répond pas.

## Tester sur l'ordinateur

Le service worker ne fonctionne qu'en `https://` ou sur `localhost`. Depuis ce dossier :

```sh
python3 -m http.server 8000
```

Puis ouvre <http://localhost:8000>. Dans Chrome ou Edge, l'icône d'installation apparaît dans la barre d'adresse (ou le bouton « Installer Alive sur cet appareil » dans le panneau).

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
