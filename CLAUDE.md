# Consignes de travail — dépôt `solidarite`

## Publication : toujours fusionner dans `main`

Le site est publié par GitHub Pages **à partir de la branche `main`** :

- https://asadgery.github.io/solidarite/marie-noelle/

Une modification poussée sur une branche de travail **n'apparaît pas en
ligne**. Donc : après chaque modification validée, fusionner
systématiquement la branche de travail dans `main` et pousser, sans
attendre qu'on le redemande.

```
git checkout main
git merge --no-ff <branche-de-travail>
git push -u origin main
```

Le déploiement Pages prend ensuite 1 à 2 minutes. Si le changement n'est
toujours pas visible après ce délai, c'est le cache du navigateur
(Ctrl+Shift+R), pas le déploiement.

## Structure du site

Tout le contenu vit dans `marie-noelle/` :

| Fichier | Rôle |
|---|---|
| `index.html` | **Page d'accueil** (seule et unique) |
| `contributions.html` | Suivi des contributions, toutes phases, système d'onglets |
| `sprint-2.html` | Note de synthèse détaillée |
| `parcours.html` | Timeline « Notre Parcours » |
| `galaxie-donateurs.html` | Visualisation 3D des donateurs |
| `accueil.html` | Redirection → `index.html` (ancienne page d'accueil) |
| `contributions-act-2.html` | Redirection → `contributions.html` (ancienne page Phase 2) |

Les deux pages de redirection sont **conservées volontairement** : leurs
URL ont circulé (groupe WhatsApp Promo 2009). Ne pas les supprimer.

## Système de design

- Police : Poppins (Google Fonts)
- Vert principal : dégradé `#56ab2f` → `#a8e063`
- Violet secondaire (encadrés informatifs / officiels) : `#667eea` → `#764ba2`
- Alerte : `#f5576c` · Attention : `#f5a623` · Succès : `#56ab2f`
- Menu latéral fixe `.sidebar` (260px), bascule en burger sous 968px
- Les encadrés suivent le patron `.<nom>-box` (`prescription-box`,
  `ministry-box`, `disease-box`, `done-box`, `phase2-box`…)

## Suivi des contributions (`contributions.html`)

Toutes les phases sont décrites dans le tableau `PHASES`, en haut du
`<script>`. Pour ajouter une phase : ajouter une entrée à ce tableau,
rien d'autre. Onglets, indicateurs et tableaux sont générés à partir de
cette configuration.

- Les Google Sheets utilisent toujours « Dose 1/2/3 » en interne
  (`csvTag`) ; le mapping vers la numérotation globale affichée
  (`globalLabel`, ex. « Dose 7 ») se fait uniquement dans `PHASES`.
- Les valeurs de `restitutions` sont des montants internes au calcul de
  report cumulé — **ne pas les déduire d'un raisonnement métier**
  (une confusion avec l'avance fournisseur a déjà causé une erreur).
- Le chargement des CSV prend quelques secondes : ce n'est pas un bug.

## Vigilance sur les chiffres

Les montants sont **dupliqués en texte libre** sur plusieurs pages, sans
source de vérité centralisée. Après toute modification d'un total,
vérifier partout :

```
grep -rn "9 600 000\|4 800 000\|9,6M\|4,8M" marie-noelle/
```

Toujours croiser dates et montants avec les pièces justificatives réelles
avant publication.

## Rendu visuel

Chromium est disponible pour vérifier une modification avant publication :

```
/opt/pw-browsers/chromium-1194/chrome-linux/chrome --headless --no-sandbox \
  --hide-scrollbars --window-size=1280,3000 \
  --screenshot=/tmp/rendu.png "file:///home/user/solidarite/marie-noelle/index.html"
```
