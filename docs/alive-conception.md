# Alive — conception et feuille de route

*Les bacs à sable cités (`src/…`) sont dans le projet Claude « Alive » ; le jeu jouable de ce dépôt est [`index.html`](../index.html).*

*Mis à jour le 8 nov. 2026. Ce document décrit l'état actuel du projet ; les essais abandonnés sont résumés à la fin.*

*Les animations (principes, marche, états, chiffres) ont leur propre document : [alive-animations.md](alive-animations.md).*

## Principe
**L'histoire d'un zombie gentil dans un monde d'horreur.** Jeu HTML5 en vue de dessus. Le héros est un **petit zombie kawaii et pataud** en pyjama raccommodé. Le jeu repose sur le contraste entre ce personnage doux et maladroit et un monde vraiment inquiétant.

- Il est **gentil** : il mange des cervelles qui poussent (jamais personne), grogne doucement (« Bwuuh… »), fait la sieste.
- Monde : cimetière au crépuscule (tombes, os, champignons, arbres morts, marais qui fait des bulles, brume au sol), et nuit d'horreur avec feux follets.
- Ne pas s'inspirer de personnages existants.

## Pitch — « Se frayer un chemin vers son enfance »
Le petit zombie se réveille dans un monde d'horreur. Pour se souvenir de l'humain qu'il était, il doit **traverser des zones peuplées de vrais monstres terrifiants et de pièges**. Il y cherche les **reliques de son enfance** (des objets de sa chambre) et les **rapporte dans sa cabane**, qui grandit avec elles. Le joueur a envie de le protéger, et c'est ce contraste qui porte le jeu.

**Ton** : les monstres font vraiment peur (taille, silhouette, bruits) mais restent dans le même style dessiné, **sans gore**. La peur vient de la menace, pas du sang.

**Deux familles de monstres**
- **Les Terreurs** : les vrais dangers. Il faut les éviter, les contourner ou les tromper. On ne les combat pas : il est trop petit et trop maladroit. Première Terreur : **L'Aveugle** (voir plus bas).
- **Les Solitaires** : des monstres tristes ou perdus, par exemple :
  - un fantôme qui a peur du noir ;
  - un squelette à qui il manque un os ;
  - une citrouille fendue ;
  - un corbeau sans voix.

  On peut les aider et devenir leur ami. En retour, ils donnent un coup de main : un passage, une info, une distraction.

**Le refuge : la cabane qui grandit avec les reliques**
- Au départ, c'est une **cabane d'enfant** :
  - un vieux drap tendu sur un manche à balai, posé entre deux croix de tombe. C'est le drap de son lit, avec les mêmes étoiles que son pyjama ;
  - une bougie à l'intérieur ;
  - des pierres sur les coins, une pièce ocre cousue, des rubans qui nouent les pans.
- **Sa lumière fait reculer les Terreurs** : c'est une zone sûre, avec une limite visible au sol.
- Il s'y glisse à quatre pattes et se blottit derrière une couverture roulée. Quand une Terreur rôde, il s'enfonce : on ne voit plus que ses yeux qui dépassent.
- C'est là qu'il se réveille après une capture.
- **Les reliques d'enfance** : il les trouve dans le monde, les porte sur sa tête et les rapporte dans la cabane. Chaque relique :
  - ajoute un morceau de sa chambre à la cabane ;
  - agrandit la lumière ;
  - réveille un souvenir : la bulle de rêve apparaît dès qu'il la ramasse ;
  - donne une émotion, qui débloque une capacité.

| Relique | Émotion | Ce qu'elle change dans la cabane | Capacité prévue |
|---|---|---|---|
| Doudou lapin | Tendresse | Tapis rond, le doudou assis sur la couverture | Calmer un monstre |
| Veilleuse-lune | Courage | Remplace la bougie : lumière plus chaude et plus forte | Sortir la nuit sans trembler |
| Boîte à musique | Joie | Guirlande lumineuse, berceuse quand il est dedans. Attention : elle tinte quand on la porte, donc elle fait du bruit | Faire fleurir le décor, ouvrir des passages |
| (à trouver) | Colère | — | Pousser les grosses pierres tombales |

- **Fin** : quand toutes les reliques sont rapportées, la cabane est devenue sa chambre entière (ou il retrouve son prénom).

**Boucle de jeu**
1. Explorer une zone.
2. Manger pour ne pas grogner.
3. Trouver une relique.
4. La rapporter à la cabane sans se faire entendre (marcher doucement, faire le mort, passer derrière les Terreurs).
5. Aider un Solitaire au passage.
6. La cabane grandit et il gagne une capacité. Passer à la zone suivante (marais, crypte, forêt morte…).

## Première Terreur : L'Aveugle
Référence : `src/terreur-anim-v0.1.html`.

**Look**
- Grande masse voûtée, deux fois la taille du petit zombie, couverte de lambeaux sombres (violet ardoise) qui se terminent en franges déchirées. Des vertèbres pâles pointent le long du dos.
- Petit crâne pâle qui pend en avant au bout d'un cou épais. **Paupières cousues** (gros points de fil violet), une grande oreille plate sur le côté, deux fentes de narines. Une bouche en fente avec de petites dents, qui s'ouvre quand il écoute ou fonce.
- **Très longs bras qui traînent en arrière**, sortis de sous la fourrure. **Mains retournées, posées sur le dos** : paume vers le ciel, dos de la main qui racle le sol, doigts qui traînent puis se recourbent vers le haut. Il les ramène devant lui pour fouiller, tâter, attraper ou se protéger de la lumière. Cou épais et souple qui s'étire vers les bruits et hoche à chaque pas lourd. Le détail des animations est dans [alive-animations.md](alive-animations.md).
- **Style (v0.2)** : même rendu que le petit zombie, esprit Ghibli / manga à l'encre : volumes doux éclairés en haut à gauche, trait d'encre plus épais côté ombre, mèches de fourrure effilées, quelques hachures dans les creux. Plus d'effet « feuille de papier » quand il se retourne : le corps garde son volume et la tête, les bras et les pieds passent par l'avant.

**Comportement**
- **Ronde** : il marche lentement entre quatre points et s'arrête à chacun pour tendre l'oreille. Ses pas lourds font trembler le sol, et le petit zombie frissonne quand il est proche. Il claque des dents pour « écouter », et souffle de la brume.
- **Il entend** : chaque bruit fait une onde ; s'il est dans l'onde, il l'entend. Sa tête se tourne d'un coup vers le bruit et de petites ondes partent de son oreille.
  - Bruit faible : il va voir, lentement.
  - Bruit fort : il fonce.
  - Sur place, il **fouille à tâtons**, bras qui balaient le sol, pendant ~3,5 s, puis reprend sa ronde.
- **Le toucher** : s'il frôle le petit zombie, il l'attrape. Sauf s'il **fait le mort** : il le tâte (petites tapes), puis l'ignore.
- **La lumière** : il s'arrête au bord de la lumière du refuge. Il grogne, la bouche ouverte, tend les bras vers la cabane, puis la lumière le fait reculer (sifflement, mains devant la tête).
- **Capture** (sans gore) : sa main se referme, il soulève le petit zombie, tout devient noir (« … il se réveille dans sa cabane »). La relique qu'il portait retourne à sa place, et L'Aveugle repart de l'autre bout de sa ronde.

**Le bruit du petit zombie** (rayon de l'onde, en unités du monde ; le zombie fait ~100 de haut)

| Source | Rayon |
|---|---|
| Pas en marchant doucement (doigt à peine poussé) | 42 |
| Pas en marchant | 82 |
| Pas en courant | 200 |
| Patauger / entrer dans l'eau | 80 / 180 |
| Retomber d'un saut | 140 |
| Se cogner (« boing ») | 220 |
| Trébucher et tomber | 240 |
| Se relever | 70 |
| Croquer / aspirer / roter | 105 / 115 / 170 |
| Grogner (tout seul ou touche G) | 160 |
| « Clac » du cou | 90 |
| Sursauter | 120 |
| Ronfler | 70 |
| Boîte à musique portée (toutes les 1,7 s) | 115 |
| Faire le mort | 0 |

Vitesses : ronde 26, il va voir 46, il fonce 88 (le zombie marche à 75 et court à 140).

## Personnage : état actuel
Référence : `src/zombie-anim-v1.0.html`, tenue par défaut « Short + pieds » (esprit pyjama).

**Tête et visage**
- Tête carrée aux coins arrondis, peau vert menthe pâle, dessinée en volume : lumière en haut à gauche, reflets, ombre douce sous le menton.
- Cheveux en bataille, pansement sur le front, couture sur la tempe.
- Un **grand œil rond** brillant et un **œil bouton** violet, cousu en croix de laine jaune pâle, à la même hauteur.
- Petite moue triste avec une dent.

**Tenue : pyjama raccommodé**
- **Tee-shirt** bleu-violet, trop grand et droit (pas évasé). Épaules basses en pente douce depuis le cou, manches jusqu'au coude. Il est long, façon ado, et couvre les hanches.
  - **Encolure** ronde qui laisse voir la peau verte, avec un col passepoilé clair.
  - **Ourlet** : il fait le tour du corps. Plus bas au centre, il remonte sur les côtés et laisse voir le dos du tee-shirt, plus sombre. Il a une encoche, un lambeau qui pend côté gauche et un coin qui tombe.
  - **Torse** mat et creux : ombre sous le col, plis qui tombent des épaules, aucun reflet rond qui le gonflerait.
- **Short** du même tissu, d'une seule pièce.
  - Le fond englobe les hanches.
  - L'**entrejambe** se voit sous le tee-shirt : un petit V renversé avec une couture au centre.
  - Il s'arrête un peu au-dessus des chevilles. Le bas est déchiré en petites dents, avec des brins effilochés.
  - Le tee-shirt fait une ombre sur le haut du short.
- **Motif de pyjama** : petites étoiles et points pâles en quinconce, sur le tee-shirt et sur le short. Le motif suit le tissu quand il bouge.
- **Raccommodages**, toujours au même endroit, qu'il regarde à gauche ou à droite :
  - une pièce carrée ocre cousue (petits points sur les côtés) sur le ventre, côté droit ;
  - une petite pièce identique sur la jambe droite du short ;
  - un petit trou qui laisse voir la peau près de l'ourlet, avec deux brins.

**Bras et mains**
- Petits bras courts.
- **Mains rondes en boule**, avec du volume (dégradé et reflet).
- En vue de 3/4, le côté vers lequel il regarde est le côté lointain :
  - le bras proche est plus clair et passe devant le torse ;
  - le bras lointain est plus sombre, avec l'épaule rentrée derrière le tee-shirt.

**Jambes et pieds**
- Petites jambes vertes, serrées. On en voit un bout entre le short et les pieds.
- **Pieds dodus et aplatis** :
  - semelle bien à plat ;
  - le dessus descend vers la pointe ;
  - petite ombre de contact sous le bout du pied.
- **Orteils toujours dans le sens de la marche** :
  - de profil : deux petits traits au bout du pied ;
  - quand il vient vers nous : trois traits au centre de l'avant ;
  - quand il s'éloigne : pas d'orteils, on voit le talon.
- **À l'arrêt, pieds en dedans**, comme un petit enfant. Il garde la dernière direction de marche.

## Animation : état actuel
- **Toujours de 3/4**, tourné à gauche ou à droite. On ne le voit de face que pendant un demi-tour, et les bras redeviennent alors symétriques.
- **Démarche** :
  - Petits pas collés au sol : le pied posé ne glisse pas, et la cadence suit la vitesse.
  - Le pied décolle vite, plane un instant, puis retombe d'un coup (« ploc »). Il s'écrase un peu en touchant le sol et soulève un petit nuage de poussière.
  - Les deux pieds font le même pas.
  - Les pieds se déroulent : pointe en haut quand ils se lèvent, pointe en bas quand ils poussent derrière.
- **Corps de mort-vivant** :
  - pas lourds : il se tasse sur le pied d'appui au lieu de rebondir ;
  - corps peu élastique ;
  - dandinement gauche-droite ;
  - dos voûté en marchant ;
  - tête toujours un peu penchée, comme un cou cassé.
- **Bras de zombie** : en marchant, les deux bras se tendent vers l'avant, plus haut quand il monte et plus bas quand il descend. Le bras proche avance son épaule pour que sa main passe devant le torse.
- **À l'arrêt** : la tête tombe lentement sur l'épaule et le corps s'affaisse. Puis il se redresse d'un coup, avec un petit « clac ».
- **Tissu** : le bas du tee-shirt suit avec un temps de retard :
  - il traîne en arrière quand il avance ;
  - il suit le dandinement et les pas ;
  - il repart vers l'avant quand il s'arrête ;
  - il s'évase quand il retombe d'un saut.

  Les pointes de l'ourlet ondulent.
- **Œil bouton** :
  - il suit la tête avec un léger retard ;
  - quand il trébuche, il se découd et pend au bout d'un fil en se balançant (dessous, on voit un œil fermé recousu). Il se recoud au bout d'environ 2 s, avec un « tic » ;
  - quand il sursaute, il fait un quart de tour et gonfle un peu.
- **Instinct cervelle** : quand une cervelle ou une limace est proche, il tourne la tête et les yeux vers elle et tend les bras plus haut.
- **Il garde un œil sur L'Aveugle** quand il est proche.
- **Mouche compagnon** (petite mouche prune aux grands yeux) :
  - elle tourne autour de sa tête quand il marche ;
  - elle se pose sur sa tête quand il attend, et il lève les yeux vers elle ;
  - elle part repérer la nourriture et tourne au-dessus ;
  - elle vient quémander les miettes quand il mange ;
  - **sentinelle** : elle s'affole et bourdonne quand L'Aveugle approche ;
  - elle se pose sur la croix de la cabane quand il est dedans, et sur lui quand il fait le mort.
- Le curseur « Pataud » (amplitude des rebonds et du dandinement) est réglé à **0,7** par défaut.

## Actions du zombie

**Faites, dans les bacs à sable**
| Action | Commande | Ce qui se passe |
|---|---|---|
| Marcher | ZQSD ou flèches (doigt glissé sur mobile) | Petits pas, bras tendus, dandinement, le tissu suit. Peu de bruit |
| Courir | Maj + direction | Pas plus longs et plus rapides, le tee-shirt traîne davantage. Très bruyant, il peut trébucher |
| Se cogner | Courir contre un obstacle | « Boing », petit recul, poussière |
| Sauter | Espace ou bouton | Il se ramasse, s'étire en l'air, puis atterrit |
| Trébucher | Bouton | Il tombe : le bras côté sol se décroche et l'œil bouton se découd. Il lâche la relique qu'il porte. Il se relève et le bras revient |
| Manger | E ou bouton | Cervelle : « gros croc » en trois bouchées, « glup », rot. Limace : aspirée façon spaghetti |
| Faire le mort | F ou bouton (F encore ou bouger pour se relever) | Il s'effondre sans bruit, yeux fermés, la mouche se pose sur lui. L'Aveugle le tâte puis l'ignore |
| Grogner | G ou bouton (et tout seul de temps en temps) | « Bwuuh… » : bruit qui attire les Terreurs |
| Porter une relique | Marcher dessus | Elle se pose sur sa tête. Il la lâche s'il trébuche ou fait le mort |
| Se glisser dans la cabane | S'arrêter devant l'ouverture (reculer pour sortir) | Il se blottit dedans ; s'il porte une relique, elle s'installe et la cabane grandit |
| S'asseoir | Tout seul après ~6 s sans bouger | Assis, les deux mains devant le ventre |
| Dormir | Bouton, ou tout seul après ~15 s assis | Il s'endort assis, avec des « z » (et il ronfle) |
| Sursauter | Réveillé par une touche quand il est assis ou endormi | Bras écartés, petit bond, l'œil bouton tourne |
| Nager / patauger | Entrer dans le marais | Bras qui pagaient, ronds dans l'eau |

**À prototyper pour le jeu**
- **Dormir dans la cabane** : sauvegarde.
- **Se cacher** dans le décor : hautes herbes, derrière une tombe…
- **Aider un Solitaire** : porter un objet, retrouver un os…
- **Utiliser les capacités** des reliques : tendresse, courage, joie, colère.

## Faim de cervelle
Il a faim comme un vrai zombie, mais il ne mange **jamais personne**.
- **Tas de cervelles** : trois cervelles roses empilées (une grosse derrière, une moyenne à droite, une petite à gauche), prises dans quelques ronces.
  - On mange d'abord la petite.
  - Une cervelle mangée repousse sous forme de bourgeon : il gonfle, tremble et fait « plop » (environ 12 s).
  - Elles remplissent beaucoup.
- **Limaces de marais** : elles vivent au bord de l'eau et fuient le zombie, lentement. Elles remplissent peu, et il faut les attraper.
- **Champignons-lanternes** : ils remplissent un peu et le font briller dans le noir. Ils ne sont pas encore dessinés.

Manger fait du bruit (croquer, roter) : il faut choisir le bon moment.

**Paliers de faim**
1. **Petit creux** : il grogne et son ventre gargouille.
2. **Grosse faim** : il marche raide et lentement, son bouton se découd plus facilement, et ses grognements plus forts attirent les Terreurs.
3. **Affamé** : ses yeux sont vides, et les Solitaires ont peur et le fuient.

Il ne meurt pas de faim. Mais tant qu'il n'a pas mangé, il perd ses amis et des bouts de corps (bras, bouton), et il devient bruyant.

## Bacs à sable
- `src/zombie-anim-v1.0.html` : le petit zombie.
  - Le bouton **Pantalon** propose plusieurs tenues : Short + pieds (par défaut), Tee + baggy, Sous la tunique, Carrés cousus, Dépareillé, Sans. Une case « Baggy un ton plus sombre » change la couleur du baggy.
  - Visages alternatifs, non retenus : Dépareillé, Grands yeux, Endormi, Pansement, Sourire, Œil qui pend.
  - Le système d'humeur (calme, joie, faim, peur, tristesse, souvenir) est dans le code, mais il n'a pas de rendu visible.
- `src/terreur-anim-v0.1.html` : L'Aveugle et la cabane-refuge.
  - Trois reliques à rapporter : le doudou (en bas à gauche, derrière le marais), la veilleuse-lune (en haut), la boîte à musique (au milieu de la ronde de L'Aveugle).
  - Case « Voir le bruit » : affiche les ondes (blanches, ou rouges quand L'Aveugle les entend).
  - Bouton « Recommencer ».
- `src/esprit-anim-v0.2.html` : l'Esprit de l'étang (direction précédente), avec le même moteur.

## À définir
- Une seule cabane qui voyage avec lui (il la remonte dans chaque zone) ou une cabane par zone ?
- La quatrième relique (Colère) et les suivantes.
- Les autres Terreurs : chacune un sens différent (une qui voit dans le noir mais n'entend rien, une qui sent l'odeur des cervelles…).
- Le premier Solitaire et ce qu'il demande.
- Les dangers du décor : pièges, eau profonde, ronces…

## Prochaines étapes
1. Régler L'Aveugle en jouant : rayons de bruit, vitesses, durée de la fouille, distance au bord de la lumière.
2. Dormir dans la cabane = sauvegarde ; se cacher dans le décor (hautes herbes, derrière une tombe).
3. Dessiner le premier **Solitaire** et sa petite quête.
4. Intégrer le tout dans le prototype de jeu : jauge de faim, paliers, première zone avec la cabane et ses reliques.

**Finitions du zombie restant à faire**
- Recaler les petites secousses de chaque pas (bras, tête) sur la nouvelle cadence, plus rapide.
- Faire passer la jambe proche du short par-dessus l'autre quand il marche.
- Ajouter une vue de dos quand il monte, et peut-être une vraie vue de face quand il descend.
- Ajouter de l'inertie aux départs et aux arrêts (petit pas de rattrapage).
- Au repos : micro-secousses irrégulières et moments où il « oublie » de bouger.
- Vérifier comment les mains tiennent la cervelle pendant le repas.
- Dessiner les champignons-lanternes.

## Essais écartés (résumé)
- **Tenue** :
  - tunique longue sans pantalon ;
  - pantalons divers : déchiré avec pieds, carrés cousus, sous une tunique courte ;
  - tee-shirt évasé en cloche avec un ourlet tout en dents de scie (effet robe) ;
  - baggy en bande fine, pattes d'éph ;
  - short brun, short en tubes autour de chaque jambe ;
  - poche de poitrine, pièce rayée cousue en croix, pièce lilas, accroc en éclair.
- **Corps** :
  - tête plus basse façon chibi ;
  - cœur visible sur la poitrine (fragments, lueur, cœur rapiécé, patchwork) ;
  - torse bombé avec un reflet rond ;
  - épaule accrochée au coin du tee-shirt.
- **Membres** :
  - botte trouée, pied nu avec orteils, jambes sans pieds ;
  - bras rallongés ;
  - mains avec doigts et pouce.
- **Animation** :
  - démarche saccadée ;
  - démarche boiteuse avec un pied traîné ;
  - œil fou qui sort de l'orbite ;
  - bave.
- **Refuge** : souvenir-refuge isolé (chaque souvenir posé seul dans le monde), cercle de veilleuse seul, maison dessinée à la craie.

## Moteur d'animation (commun aux bacs à sable)
- Canvas 2D. Les personnages sont dessinés en code ; le zombie dans un repère de 140×140, avec les pieds à y≈132.
- Ressorts : « gelée » du corps, bras, tête, œil bouton, tissu du tee-shirt ; mains de L'Aveugle (bras en cinématique inverse, deux segments).
- États du zombie : repos, marche, course, cogne, saut, trébuche, au sol, se relève, mange, assis, dort, surpris, nage ou patauge, fait le mort, attrapé.
- États de L'Aveugle : ronde, pause d'écoute, écoute, va voir, fonce, fouille, bord de la lumière, recule, tâte, attrape, retour.

## Historique
- **Esprit de l'étang** (direction précédente) : têtard-esprit kawaii dans l'esprit Ghibli, mousse qui pousse au fil des jours, lueur la nuit.
- **Ogg humain** (abandonné) : homme des cavernes en caleçon.
- **Prototype de jeu v0.1** (Ogg humain) :
  - un seul fichier HTML ;
  - monde de 2000×2000 généré par graine ;
  - jauges de faim et de vie ;
  - buissons de baies ;
  - cycle jour/nuit de 150 s.
