# Qālūn ʿan Nāfiʿ — texte Unicode coloré (tajwīd)

Texte intégral de la riwāya de Qālūn, page par page, avec pour chaque lettre la couleur
de tajwīd **relevée dans un mushaf imprimé** (et non calculée), et les signes de waqf de ce
mushaf. Conçu pour être affiché dans une application sur **son propre fond** : aucune image,
aucune couleur de fond ; les lettres sans couleur prennent la couleur de texte de l'application.

## Contenu

| Fichier | Rôle |
|---|---|
| `data/qaloon_mushaf.json` | 604 pages : sourates, versets (`first_word`, `last_word`), texte. |
| `data/qaloon_colours.json` | Couleur de chaque lettre colorée : `mot → [début, fin, encre, rule_agrees, rgb]`. |
| `data/qaloon_waqf.json` | Signe de waqf imprimé après chaque mot concerné : `mot → signe`. |
| `data/qaloon_mushaf.sqlite` | Les mêmes données (tables `pages`, `surahs`, `ayahs`, `page_ayahs`, `words`, `letter_colours`, `waqf`, `inks`). |
| `docx/Qaloon_texte_couleur.docx` | Lecture dans Word (texte seul). |
| `fonts/QaloonWaqf-Regular.ttf` | Signes de waqf ۖ ۗ ۘ ۙ ۚ ۛ (dérivée d'Amiri Quran, licence OFL). |
| `example/index.html` | Exemple d'affichage sur fond transparent. |
| `images/transparent/001.png` … `604.png` | Pages du mushaf en image, **sans cadre et sans fond** (PNG transparent) : texte, couleurs, rosaces, signes et bandeaux tels qu'imprimés. |
| `images/crop_boxes.json` | Rectangle découpé dans chaque page du scan d'origine. |

### Images transparentes

Chaque pixel garde la couleur de l'encre imprimée ; la part du pixel couverte par l'encre
devient la transparence (le papier disparaît, les contours restent lisses). Posez l'image
directement sur un fond clair. L'encre étant sombre, sur un thème sombre posez-les sur un
fond clair couleur papier.
Ces images proviennent du scan d'un mushaf imprimé : dépôt à garder privé.

## Polices

1. **KFGQPC Qaloun Uthmanic Script** — obligatoire pour le texte (caractères propres à
   Qālūn). Sa licence interdit de la redistribuer : téléchargez-la sur
   <https://fonts.qurancomplex.gov.sa/> et installez-la / intégrez-la selon ses conditions.
2. **Qaloon Waqf** (fournie) — en police de secours pour les signes ج ∴ لا que la première
   ne contient pas. En CSS : `font-family: "KFGQPC Qaloun Uthmanic Script", "Qaloon Waqf";`

## Afficher une page

- Mots d'une page : table `words` (`page = N`), dans l'ordre de `id`, séparés par une espace.
- Pour chaque mot, découper le texte aux positions `début`/`fin` de `letter_colours` et
  colorer ces parties avec `rgb` (la couleur mesurée dans le mushaf). Le reste du mot garde la
  couleur de texte de votre application : clair sur fond sombre, sombre sur fond clair.
- Ajouter le signe de `waqf` (s'il existe) juste après le mot, sans espace.
- Fin de verset : `ayahs.surah/ayah`, numéro affiché à la fin du dernier mot du verset.

Sur fond sombre, certaines encres du mushaf (bleu marine, bordeaux) sont peu lisibles :
vous pouvez remplacer `rgb` par une couleur de votre thème pour la même `encre`.

## Encres (légende du mushaf)

| encre | légende |
|---|---|
| `maroon` | مد 6 حركات لزوما |
| `red` | مد متوسط 4 حركات |
| `orange` | مد 2 أو 4 أو 6 جوازا |
| `brown` | مد حركتان |
| `green` | إخفاء ومواقع الغنة |
| `grey` | إدغام وما لا يلفظ |
| `navy` | تفخيم الراء |
| `blue` | قلقلة |

## Fiabilité

Les couleurs ont été lues automatiquement dans un scan et reportées sur le texte Unicode.
`rule_agrees = false` signale une couleur présente dans le scan mais placée sans règle de
tajwīd qui la confirme : à relire. Une relecture ligne par ligne est en cours ; les lignes
vérifiées sont listées dans `qaloon_colours.json → reviewed_lines`.

## Sources et licences

- Texte Qālūn : édition Unicode du Complexe du Roi Fahd (KFGQPC), via text.quran.ws. Le
  texte arabe doit être conservé à l'identique ; vérifiez les conditions de l'éditeur avant
  toute diffusion publique.
- Positions des signes de waqf : texte ʿUthmānī de Tanzil (<https://tanzil.net>), CC BY 3.0.
- Police Qaloon Waqf : dérivée d'Amiri Quran, SIL Open Font License 1.1.
