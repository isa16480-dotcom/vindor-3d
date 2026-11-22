# Vindor 3D — exploration en vue 3D pour Foundry VTT / The Forge

Tu poses ton jeton sur la carte, tu fais un clic droit sur ton jeton puis tu cliques sur le bouton **Vue 3D** (casque), ou tu appuies sur **V**, et tu
apparais **à l'emplacement exact de ton jeton**, en vue 3D à la troisième personne. Tu marches dans la ville,
et ton jeton se déplace en même temps sur la carte 2D pour toute la table. Les autres jetons de la scène
apparaissent en 3D (figurine par défaut ou ton propre modèle `.glb`).

Compatibilité : Foundry VTT v12 et v13 (donc The Forge).

> Création de fan non officielle, inspirée de l'univers de Runeterra. Sans lien avec Riot Games.
> Les bâtiments de la cité ont été générés pour ce projet. Textures photo, arbres, statues, buissons,
> rochers, caisses et tonneaux : [Poly Haven](https://polyhaven.com) (licence CC0, domaine public).

## Nouveautés de la version 0.4 : garde chevalier animé
- Modèle 3D fourni : **Garde chevalier** (armure de plaques, heaume fermé, écharpe et pan de tissu bordeaux, épée),
  avec trois animations : repos, marche, course.
- Sur un jeton : clic droit → bouton **cube** (Modèle 3D) → *Modèle fourni* → « Garde chevalier ».
- Les animations suivent la vitesse : un jeton déplacé de quelques cases **marche tranquillement**,
  plus loin il court pour rattraper sa place, et il se met au repos à l'arrêt.
- Ton propre modèle `.glb` animé marche aussi : nomme ses animations *Idle*, *Walk* et *Run*.

## Nouveautés de la version 0.3 : jour, nuit et brouillard
- Outil MJ **Ambiance 3D** (icône nuage et lune, barre d'outils Jetons) : *Jour*, *Soir*, *Nuit*, ou
  **Suivre l'obscurité de la scène**. Avec ce dernier choix, la 3D passe du jour à la nuit en même temps que la carte 2D,
  y compris quand un module d'heure ou de météo assombrit la scène.
- **Brouillard** : aucun, léger ou épais. On voit mal devant soi et autour, et des nappes de brume flottent autour du personnage.
- La nuit : étoiles, lune, fenêtres allumées, torches et braseros plus lumineux.
- Tout le monde voit la même ambiance. Le changement se fait en douceur, sans recharger la 3D.
- Pour une macro : `game.modules.get("vindor-3d").api.setAmbience("night", 2)`
  (heure `"auto"`, `"day"`, `"dusk"`, `"night"` ; brouillard `0`, `1` ou `2`).

## Nouveautés de la version 0.2 (cité réaliste)
- Bâtiments aux arêtes arrondies, vraies fenêtres (encadrements en pierre, croisillons, vitres, volets), portes en planches.
- Textures photo : brique, pierre, enduit, ardoise, tuiles, pavés, bois, fer, terre, herbe, falaises.
- Torches murales et braseros avec de **vraies flammes animées** qui éclairent les murs autour de toi.
- Statues équestres en bronze, vrais arbres feuillus, herbe qui ondule au vent, fougères, buissons, rochers moussus.
- Version détaillée près de toi, version allégée au loin : la ville reste fluide.

## Commandes

| Touche | Action |
|---|---|
| Z / W ou ↑ | avancer |
| S ou ↓ | reculer |
| Q / A ou ← | aller à gauche |
| D ou → | aller à droite |
| Maj | courir |
| Espace | sauter |
| Clic + glisser | tourner la caméra |
| Molette | zoom (jusqu'à la vue presque à la 1re personne) |
| V ou Échap | revenir à la carte 2D |

ZQSD et WASD marchent tous les deux : le module lit la position physique des touches (clavier AZERTY ou QWERTY).

## Pour le MJ

Dans la barre d'outils **Jetons** :
- **Créer la scène Vindor** (icône tour d'échecs) : crée la scène avec la carte vue du dessus de la cité, déjà reliée au monde 3D.
- **Configurer la 3D de la scène** (icône ville) : relie une scène à un monde 3D.
  - *Utiliser Vindor* pour la cité fournie ;
  - ou ton propre modèle `.glb` + le carré (en mètres) que couvre l'image de fond.
- **Vue 3D** (icône cube) : ouvrir / fermer (touche **V**, modifiable dans *Configurer les contrôles*).

Sur chaque jeton (clic droit → HUD) : bouton **casque** = passer ce jeton en vue 3D ; bouton **cube** = choisir un **modèle 3D (.glb)**, sa taille en mètres et une échelle.
Si le modèle contient des animations nommées *Idle*, *Walk* ou *Run*, elles sont jouées automatiquement.

Réglages du module : qualité (basse / moyenne / haute), ouverture automatique de la 3D en arrivant sur une scène 3D,
vitesse de marche, rotation du jeton 2D.

**Changer de carte** : quand Foundry t'emmène sur une autre scène (le MJ, ou une région de téléportation),
la vue 3D se recharge sur la nouvelle scène si elle a un monde 3D.

## Installation

### Sur The Forge (ou tout Foundry en ligne)
Foundry installe les modules à partir d'une **adresse de manifeste** (`module.json` en ligne). Le plus simple :
1. Crée un dépôt GitHub public `vindor-3d`.
2. Crée une *Release* (ex. `v0.1.0`) et joins-y **`module.json`** et **`vindor-3d.zip`**.
3. Dans `module.json`, remplis avant de le joindre :
   - `"manifest": "https://github.com/isa16480-dotcom/vindor-3d/releases/latest/download/module.json"`
   - `"download": "https://github.com/isa16480-dotcom/vindor-3d/releases/latest/download/vindor-3d.zip"`
4. Sur The Forge : *Bazaar* / *Setup → Add-on Modules → Install Module* → colle l'adresse du manifeste → *Install*.
5. Active **Vindor 3D** dans ton monde (*Gérer les modules*).

### Foundry installé sur ton PC
Décompresse `vindor-3d.zip` dans `Données Foundry/Data/modules/vindor-3d/`, relance Foundry, active le module.

## Bon à savoir
- La bibliothèque 3D (three.js) est chargée depuis Internet (jsDelivr) à l'ouverture de la vue 3D.
- La ville fait environ 33 Mo (modèles compressés + textures). Le premier chargement prend un peu de temps,
  ensuite le navigateur la garde en cache.
- Chaque joueur affiche la 3D sur son propre ordinateur : une carte graphique correcte aide.
  Si c'est lent, mets la qualité sur *Moyenne* (moins d'herbe et de détails) ou *Basse* (pas d'herbe, pas d'ombres).
- Le dossier `test/` contient un banc d'essai hors Foundry (`test/index.html`, à ouvrir via un petit serveur web local).
