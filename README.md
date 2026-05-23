# Ranker

> Classez n'importe quoi, un duel à la fois.

**Ranker** est une application web autonome — un seul fichier HTML, aucune dépendance, aucune installation, utilisable hors ligne. Collez une liste, répondez à des duels, obtenez un classement ordonné et exportable.

---

## Aperçu

```
Vacances à Lisbonne
Apprendre le piano        →   18 éléments   →   ~34 duels   →   Classement final
Lancer un side-project
...
```

Chaque duel oppose deux éléments. Vous choisissez le meilleur. L'algorithme calcule un classement précis à partir de vos réponses.

---

## Fonctionnement

### Algorithme

L'application combine un **planning de duels en 4 passes** avec un système de **score Elo à K variable** :

| Passe | Logique | But |
|-------|---------|-----|
| 1 — Shuffle | Paires aléatoires | Première couverture, chaque item comparé au moins une fois |
| 2 — Voisins | Tri Elo → paires consécutives (1v2, 3v4…) | Affine le classement local |
| 3 — Cross-band | Top half vs bottom half | Valide les grandes séparations |
| 4 — Skip-one | (1v3, 2v4…) | Comble les angles morts des passes précédentes |

Pour `n` éléments → environ `2n` comparaisons. Exemple : 18 éléments → ~34 duels.

Le **K Elo est décroissant** : élevé en début de session (convergence rapide), plus faible ensuite (stabilisation). Les égalités sont supportées et intégrées dans le calcul.

En cas d'égalité de score Elo, le classement est départagé par nombre de victoires, puis taux de victoires, puis nombre de défaites.

---

## Utilisation

1. Ouvrez `ranker.html` dans n'importe quel navigateur moderne
2. Collez votre liste (un élément par ligne)
3. Répondez aux duels
4. Exportez le classement

Aucun serveur, aucune connexion internet requise.

---

## Raccourcis clavier

| Touche | Action |
|--------|--------|
| `←` | Choisir l'élément de gauche |
| `→` | Choisir l'élément de droite |
| `⌫ Backspace` | Annuler le dernier choix |

---

## Export

- **Markdown** — liste numérotée avec scores, prête à coller
- **JSON** — tableau d'objets `{ rank, title, score, wins, losses, ties, comparisons }`

---

## Compatibilité

Navigateurs modernes (Chrome, Firefox, Safari, Edge). Pas d'installation, pas de build, pas de dépendances.

---

## Licence

MIT
