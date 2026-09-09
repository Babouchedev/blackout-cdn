# CDN BlackOut — arborescence à remplir

Généré le 2026-09-09 à partir du code de la base (`resources/[Core]/core`).

## À quoi ça sert

La base appelle ses images sur un CDN externe qui est **mort** (`cdn.99vf.fr`).
Ce dossier reproduit **exactement** l'arborescence que ton CDN doit avoir.
Tu déposes les images dedans (au fur et à mesure), puis tu uploades le tout.

## Comment l'utiliser

1. Tu remplis les dossiers avec tes images (voir les 2 listes ci-dessous)
2. Tu uploades le contenu de ce dossier à la **racine de ton CDN**
3. Dans le code, tu remplaces l'ancienne adresse par la tienne :
   - `https://cdn.99vf.fr/3838384859/` → `https://TON-CDN/`
   - (~460 occurrences : ~290 dans les `.lua`, le reste dans `interface/build/assets/index-*.js` et le `.css`)
   - Dis-le moi quand tu es prêt, je fais le remplacement automatiquement.

> ⚠️ L'adresse actuelle contient un identifiant : `cdn.99vf.fr/**3838384859**/assets/...`
> Ici l'arborescence part **après** ce `3838384859`. Donc `assets/banking/logo.png` ici
> = `https://TON-CDN/assets/banking/logo.png` une fois en ligne.

## Les 2 listes

| Fichier | Contenu |
|---|---|
| `_FICHIERS-ATTENDUS.txt` | **156 fichiers nommés en dur** dans le code, groupés par dossier. Ce sont les plus importants : sans eux, un menu précis est cassé. |
| `_ITEMS-ATTENDUS.txt` | **1008 icônes d'items** (`items/<nom>.webp`), extraites de `core/items.lua`. C'est le gros du volume. |

## Dossiers "dynamiques"

Certains chemins sont construits au moment de l'exécution — le dossier est connu,
le nom du fichier dépend des données du jeu :

| Dossier | Nom de fichier attendu |
|---|---|
| `items/` | `<nom_item>.webp` — voir `_ITEMS-ATTENDUS.txt` (1008) |
| `assets/PED/` | `<label_du_ped>.png` |
| `assets/interacts/` | `<nom_icone>.svg` |
| `vehicules/` | `<modele>.webp` |
| `BoutiqueVehicules/vision/` | `<modele>.webp` |
| `assets/catalogues/headers/` | `header_<nom>.webp` |
| `assets/hud/microphone_` | `microphone_<type>.png` |
| `assets/gestion-serveur/crew/` | `<type>.svg` |
| `assets/boutique/` | `<nom>.png` |
| `outfits_greenscreener/` | `<a>/<b>/<c>/<d>.webp` (4 niveaux) |
| `old_a_trier/policebadge/` | `<nom>.png` |
| `assets/map/satelite/` | tuiles de carte `{z}/{x}/{y}.png` — **potentiellement des milliers**, à traiter en dernier |

## Ordre conseillé pour remplir

1. **`assets/hud/`** + **`assets/icons/`** → visible en permanence à l'écran
2. **`items/`** → l'inventaire (le plus gros impact visuel)
3. **`assets/radialmenus/`** → le menu roue
4. **`assets/inventory/`**, **`assets/banking/`** → menus les plus utilisés
5. **`assets/jobmenu/`**, **`assets/catalogues/`**, **`assets/boutique/`** → menus métiers/magasins
6. Le reste au fil de l'eau
7. **`assets/map/satelite/`** en tout dernier (volume énorme, purement cosmétique)

## Astuce

Un fichier manquant = image cassée, **pas un crash**. Tu peux donc mettre le serveur
en ligne avec un CDN partiellement rempli et compléter petit à petit.

Pour éviter les icônes cassées en attendant, tu peux mettre une image
"placeholder" générique et la dupliquer sous tous les noms manquants.
