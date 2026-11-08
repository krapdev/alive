# Alive — animations

*Les bacs à sable cités (`src/…`) sont dans le projet Claude « Alive » ; le jeu jouable de ce dépôt est [`index.html`](../index.html).*

*Document de référence des animations, créé le 8 nov. 2026. Il décrit ce qui est en place dans les bacs à sable, avec les principes communs, les chiffres utiles et ce qui reste à faire. La conception générale est dans [alive-conception.md](alive-conception.md).*

Bacs à sable :
- Petit zombie : `src/zombie-anim-v1.0.html`.
- L'Aveugle, la cabane et les reliques : `src/terreur-anim-v0.1.html`.

---

## 1. Principes communs

**Vue de 3/4, sans effet « feuille de papier »**
- Les personnages sont vus de 3/4, tournés à gauche ou à droite. On ne les voit de face que pendant un demi-tour.
- Pendant un demi-tour, le corps ne s'aplatit jamais. Il garde son volume, et ce sont la tête, les bras et les pieds qui passent par l'avant (ils se rapprochent du centre, puis repartent de l'autre côté).
- **Le côté vers lequel il regarde est le côté lointain.** Les membres du côté proche sont plus clairs ; ceux du côté lointain sont plus sombres, un peu plus petits et un peu plus haut à l'écran (plus loin dans la profondeur).

**Ordre de dessin (du fond vers l'avant)**
- Le membre lointain est toujours dessiné avant le corps, et le membre proche après.
- **La jambe de devant reste toujours au premier plan** par rapport à la jambe du fond, même quand la jambe du fond passe devant pendant le pas.
- Le zombie : jambe du fond → jambe de devant → short / tee-shirt → bras du fond (épaule rentrée derrière le tee-shirt) → bras proche (devant le torse) → tête.
- L'Aveugle :
  1. bras du fond ;
  2. jambe du fond ;
  3. bras proche, quand il traîne en arrière (il sort de sous la fourrure) ;
  4. jambe de devant ;
  5. corps ;
  6. cou et tête ;
  7. bras proche, quand il est devant lui (fouiller, tâter, attraper, se protéger).

**Pieds collés au sol**
- La cadence suit la vitesse : un cycle (deux pas) fait deux longueurs de pas. Le pied posé recule exactement à la vitesse du corps, donc il ne glisse pas.
- Le pied décolle vite, plane un instant et retombe d'un coup. À l'impact, il s'écrase légèrement et soulève un peu de poussière.
- Chaque impact déclenche une petite secousse qui remonte dans le corps (gelée, bras, tête).

**Ressorts**
- Tout ce qui est souple suit sa cible avec un ressort amorti (léger retard, petit dépassement) : gelée du corps, bras, tête, œil bouton, tissu, cou et mains de L'Aveugle.
- Les impulsions (pas, chute, saut) s'ajoutent à la vitesse du ressort, jamais à la position : le mouvement reste continu.

**Style de rendu (Ghibli / manga à l'encre)**
- Volumes doux éclairés en haut à gauche, reflet discret, ombre douce dessous.
- Trait d'encre : fin partout, plus épais côté ombre (bas et arrière).
- Quelques hachures d'encre dans les creux. Mèches (cheveux, fourrure) en formes pleines et effilées, pas en simples traits.
- Les mèches ont une forme fixe : elles se balancent ensemble, lentement, mais ne changent pas de forme d'une image à l'autre (sinon elles scintillent).

---

## 2. Le petit zombie

Réglage général : curseur « Pataud » à **0,7** (amplitude des rebonds et du dandinement).

**Marche et course**
- Pas de **15** en marche et **19** en course (unités du monde ; le zombie fait ~100 de haut). Vitesse 75 en marche, 140 en course.
- Levée du pied basse (environ 3,6 × (0,6 + 0,6 × pataud)).
- Le pied se déroule : pointe en haut quand il se lève, pointe en bas quand il pousse derrière.
- Le corps se tasse sur le pied d'appui au lieu de rebondir (pas lourds).
- Il se dandine de gauche à droite, le dos voûté vers l'avant.
- En courant, les pas sont plus longs, le tee-shirt traîne davantage, et il peut trébucher de temps en temps.

**Orientation des pieds**
- En marche, les orteils pointent toujours dans le sens de la marche (angle lissé ; un demi-tour passe par l'avant).
- De profil : deux traits d'orteils au bout du pied. Vers nous : trois traits au centre. Vers le fond : pas d'orteils, on voit le talon.
- À l'arrêt, pieds en dedans comme un petit enfant, dans la dernière direction de marche.

**Bras**
- En marchant, les deux bras se tendent vers l'avant, plus haut quand il monte et plus bas quand il descend. Petite oscillation à chaque pas.
- Le bras proche avance son épaule pour que sa main passe devant le torse.
- Pendant un demi-tour, les deux bras redeviennent symétriques.

**Tête et cou**
- Tête toujours un peu penchée, comme un cou cassé.
- À l'arrêt, la tête tombe lentement sur l'épaule (~2,6 s), reste un instant, puis se redresse d'un coup avec un « clac ».
- Instinct cervelle : quand de la nourriture est proche, il tourne la tête et les yeux vers elle.
- Il garde un œil sur L'Aveugle quand il est proche.

**Tissu**
- Le haut du tee-shirt reste cousu au corps ; le bas suit avec un temps de retard.
- Il traîne en arrière quand il avance, suit le dandinement et les pas, repart vers l'avant à l'arrêt et s'évase en retombant d'un saut. Les pointes de l'ourlet ondulent.

**Œil bouton**
- Il suit la tête avec un léger retard.
- Chute : il se découd, pend au bout d'un fil et se balance, puis se recoud au bout de ~2 s avec un « tic ».
- Sursaut : quart de tour et petit gonflement.

**États et actions**
| État | Durée / déclenchement | Animation |
|---|---|---|
| Repos | — | Léger balancement, tête qui tombe puis « clac », grognement de temps en temps |
| Assis | après ~6 s sans bouger | Il s'assoit, mains devant le ventre |
| Dort | après ~15 s assis, ou bouton | Yeux fermés, respiration lente, « z » (il ronfle : bruit) |
| Saut | Espace | Il se ramasse (0,12 s), s'étire en l'air, atterrit avec poussière |
| Trébuche | bouton ou en courant | Il bascule en 0,28 s autour du pied avant ; le bras côté sol se décroche, l'œil se découd ; au sol ~1,15 s, se relève en 0,42 s et le bras revient |
| Fait le mort | F | Il s'effondre en 0,32 s, sans bruit, yeux fermés ; la mouche se pose sur lui ; F ou bouger pour se relever |
| Mange | E | Cervelle : trois bouchées, « glup », rot (2 s). Limace : aspirée façon spaghetti (1,5 s) |
| Sursaute | réveillé par une touche | Bras écartés, petit bond (0,45 s), l'œil tourne |
| Patauge | dans le marais | Bras qui pagaient, ronds dans l'eau |
| Attrapé | L'Aveugle le touche | Soulevé, jambes qui gigotent, yeux ronds, puis fondu au noir |
| Dans la cabane | s'arrêter devant l'ouverture | On ne voit que sa tête blottie derrière la couverture ; il s'enfonce jusqu'aux yeux quand L'Aveugle rôde |
| Porte une relique | marcher dessus | Relique posée sur sa tête, qui suit sa tête et se balance |

**Mouche compagnon**
- Vol « fonce puis fait du sur-place » autour de sa tête.
- Elle se pose sur sa tête quand il attend (il lève les yeux vers elle), part repérer la nourriture, quémande les miettes.
- Elle s'affole et bourdonne quand L'Aveugle approche.
- Elle se pose sur la croix de la cabane quand il est dedans, et sur lui quand il fait le mort.

---

## 3. L'Aveugle

Grande masse voûtée, deux fois la taille du zombie. Tout se fait lentement et lourdement, sauf la tête, qui réagit d'un coup.

**Marche lourde**
- Pas de **36**, levée du pied **11**. Vitesses : ronde 26, il va voir 46, il fonce 88.
- Le corps monte quand la jambe passe et retombe d'un coup au contact.
- À chaque pas, il bascule un peu vers l'avant puis se redresse, et s'écrase légèrement sous son poids.
- Les pieds se déroulent : le talon décolle (pointe vers le bas), la pointe se relève avant de reposer, puis le pied s'écrase à plat.
- Le genou avance quand le pied se lève.
- La jambe du fond est posée un peu plus haut et plus petite ; la jambe de devant reste toujours au premier plan.
- Chaque pas : bruit sourd, poussière, sol qui tremble (le petit zombie frissonne s'il est à moins de 300).
- Le bas de la fourrure traîne derrière le mouvement et tressaute à chaque pas.

**Bras : ils traînent en arrière**
- Par défaut (ronde, pause, écoute, va voir, fonce, bord de la lumière), les bras traînent derrière lui. Ils sortent de sous la fourrure.
- **Les mains sont retournées, posées sur le dos** : paume vers le ciel, dos de la main qui racle le sol, doigts qui traînent à plat puis se recourbent vers le haut et bougent à peine.
- Les mains suivent dans le monde, pas collées au corps : elles glissent au sol avec du retard et soulèvent un peu de poussière. Plus il va vite, plus elles traînent loin derrière.
- Il les ramène devant lui seulement pour fouiller à tâtons (elles balaient le sol), tâter un zombie qui fait le mort, l'attraper, ou se protéger de la lumière (mains devant la tête).
- Attention au toucher : son corps, sa tête et ses mains qui traînent attrapent le zombie.

**Cou et tête**
- Cou épais et souple, courbé comme celui d'un vautour, avec des plis d'encre en travers. Il part du haut du corps et suit la tête : il s'étire, se courbe, se rentre.
- La position de la tête suit un ressort souple (léger dépassement) :

| Situation | Tête |
|---|---|
| Ronde | Presque au repos, léger balancement lent |
| Pause | Balance doucement, à l'écoute |
| Il entend | Cou tendu vers l'avant et vers le haut, tête qui pivote d'un coup vers le bruit, mâchoire entrouverte, claquements de dents |
| Il va voir / fonce | Tête en avant ; en fonçant, basse et bouche grande ouverte |
| Il fouille | Tête basse vers le sol, qui oscille |
| Bord de la lumière | Tête tendue vers la cabane, qui renifle, bouche qui claque |
| Recule | Cou rentré, tête relevée en arrière, bouche grande ouverte (sifflement) |
| Il tâte | Tête baissée vers le zombie |

- À chaque pas lourd, la tête hoche (elle descend puis remonte avec un peu de retard).
- Brume de souffle toutes les ~3 s. Petites ondes qui partent de l'oreille quand il entend un bruit.

**États**
| État | Durée | Comportement |
|---|---|---|
| Ronde | — | Marche entre quatre points |
| Pause | 2,4 s à chaque point | Tête qui balance, claquements de dents |
| Écoute | 0,8 s | Se fige, tête vers le bruit |
| Va voir / fonce | jusqu'au bruit (10 s max) | Bruit faible : il va voir. Bruit fort : il fonce |
| Fouille | 3,6 s | Mains qui balaient le sol devant lui, tête basse |
| Bord de la lumière | 2,6 s | S'arrête loin de la cabane, grogne, tend la tête |
| Recule | 1,7 s | Sifflement, mains devant la tête, il recule |
| Tâte | 2 s | Petites tapes sur le zombie qui fait le mort, puis l'ignore 6 s |
| Attrape | ~1 s | La main se referme, il soulève le zombie, fondu au noir |
| Retour | — | Revient au point de ronde le plus proche |

---

## 4. Le refuge, les reliques, les effets

**Cabane**
- Le drap bouge quand il entre ou sort.
- La bougie tremble ; la lumière au sol vacille un peu (moins avec la veilleuse).
- La guirlande scintille ; des notes s'envolent de la boîte à musique quand il est dedans.
- Quand une relique est déposée : la lumière grandit doucement, pulse, étincelles, et l'émotion s'affiche en grand.

**Reliques**
- Au sol : elles flottent dans une lueur dorée, avec trois petites étoiles qui tournent.
- **Quand il en ramasse une : bulle de rêve** (image floue de sa vie d'avant), « boum » et carillon. La relique se pose sur sa tête.
- La boîte à musique portée tinte toutes les 1,7 s (bruit).

**Bruit**
- Chaque bruit fait une onde au sol : blanche, ou rouge quand L'Aveugle l'entend. Les rayons sont dans le document de conception.

**Capture**
- Le noir se referme sur le zombie (0,9 s), écran noir avec « … il se réveille dans sa cabane » (1,7 s), puis le noir s'ouvre sur la cabane (1,1 s).

---

## 5. À faire

**Petit zombie**
- Recaler les secousses de chaque pas (bras, tête) sur la cadence plus rapide.
- Faire passer la jambe proche du short par-dessus l'autre.
- Vue de dos quand il monte, et peut-être une vraie vue de face quand il descend.
- Inertie aux départs et aux arrêts (petit pas de rattrapage).
- Au repos : micro-secousses irrégulières, moments où il « oublie » de bouger.

**L'Aveugle**
- Valider en jeu la marche, le cou et les mains retournées ; régler le hochement de tête.
- Demi-tour : faire pivoter le cou et les épaules, pas seulement rapprocher la tête du centre.
- Fouille : faire traîner une main pendant que l'autre balaie.
- Vue de dos et de face quand il monte ou descend.

**Cabane**
- Animation d'entrée et de sortie à quatre pattes (pour l'instant il disparaît dans l'ouverture).
- Dormir dans la cabane (sauvegarde).
