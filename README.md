# Audit organisationnel — Grille d'auto-évaluation sécurité & conformité

Classeur Excel permettant de piloter un **audit
organisationnel de sécurité de l'information** sur la base de plusieurs
référentiels reconnus. Il sert à **positionner l'organisation** contrôle par
contrôle, à **suivre l'avancement** d'un plan d'action et à obtenir
automatiquement un **taux de couverture** global et par référentiel.

Deux niveaux de lecture sont proposés :

- une **synthèse par formules** qui se recalcule en temps réel (`Synthèse`) ;
- une **analyse croisée** via une table consolidée (Power Query) et un
  **tableau croisé dynamique** (`Ajouter1` + `TCD`).

---

## À quoi ça sert

- **Faire un état des lieux** de la posture sécurité de l'organisation face à
  des référentiels de place (ANSSI, ISO, CIS) et à la réglementation (RGPD).
- **Prioriser** : identifier ce qui n'est pas commencé, ce qui pose problème et
  ce qui est déjà en place.
- **Suivre un plan d'action** dans le temps grâce à une colonne dédiée.
- **Communiquer** : la feuille de synthèse fournit un tableau de bord chiffré,
  et le TCD permet de croiser librement les données pour un rapport d'audit ou
  un comité de pilotage.

---

## Contenu du classeur

Le fichier contient **8 feuilles** : deux vues de pilotage, cinq référentiels
et une table de consolidation.

| Feuille | Rôle | Nb de contrôles | Identifiants |
|---|---|---|---|
| `Synthèse` | Tableau de bord global (formules, temps réel) | — | — |
| `TCD` | Tableau croisé dynamique (analyse à la demande) | — | — |
| `ANSSI - Hygiène` | Guide d'hygiène informatique de l'ANSSI | 42 | `M1` … `M42` |
| `ANSSI - Admin` | Recommandations pour l'administration sécurisée des SI | 77 | `R1` … `R71` (+ variantes) |
| `ISO 27001-2022` | Mesures de l'Annexe A (ISO/IEC 27001:2022) | 93 | `A.5.x` … `A.8.x` |
| `CIS v8` | CIS Critical Security Controls v8 | 153 | `1.1` … `18.5` |
| `RGPD` | Obligations RGPD par article | 23 | `Art.5` … `Conservation` |
| `Ajouter1` | Consolidation Power Query des 5 référentiels | 388 lignes | — |

Total : **388 contrôles** répartis sur les 5 référentiels.

---

## Structure d'une feuille de référentiel

Chaque feuille de référentiel est construite de la même manière, autour d'un
**tableau Excel structuré** (`TblHygiene`, `TblAdmin`, `TblISO`, `TblCIS`,
`TblRGPD`).

Colonnes à renseigner :

| Colonne | Rôle |
|---|---|
| **Identifiant** | Code du contrôle (pré-rempli) |
| **Intitulé de la recommandation / contrôle** | Libellé du contrôle (pré-rempli) |
| **Périmètre** | Liste déroulante : `Retenue` · `Exclue` · `n.a.` |
| **Niveau de mise en œuvre** | Liste déroulante : `Totalement mis en œuvre` · `Partiellement mis en œuvre` · `Pas commencé` · `Problème !` · `n.a.` |
| **Plan d'action / Commentaires** | Texte libre (actions, responsable, échéance…) |
| **Justification (si exclue / n.a.)** | Pourquoi le contrôle est écarté |
| **Références** | Liens ou renvois documentaires |

À droite du tableau, un **bloc récapitulatif** recompte automatiquement les
contrôles par périmètre et par statut, et calcule le taux de couverture de la
feuille. **Ce bloc est calculé : ne pas le modifier à la main.**

---

## Légende

**Périmètre**

- `Retenue` — le contrôle s'applique et **compte dans le taux de couverture**.
- `Exclue` — le contrôle est volontairement écarté (justification attendue).
- `n.a.` — non applicable au contexte.

**Niveau de mise en œuvre**

- `Totalement mis en œuvre` — en place (compte pour 1).
- `Partiellement mis en œuvre` — partiel (compte pour 0,5).
- `Pas commencé` — rien de fait.
- `Problème !` — écart / blocage à traiter en priorité.
- `n.a.` — sans objet pour ce contrôle.

---

## Comment est calculé le taux de couverture

Le taux ne porte **que sur les contrôles `Retenue`** (les contrôles `Exclue` et
`n.a.` sont ignorés au dénominateur). Un contrôle partiel compte pour moitié :

```
Taux (%) = (Nb « Totalement mis en œuvre » + 0,5 × Nb « Partiellement mis en œuvre »)
           ────────────────────────────────────────────────────────────────────────  × 100
                              Nb de contrôles « Retenue »
```

Ce calcul est réalisé par des formules `COUNTIF` / `COUNTIFS` dans chaque
feuille, puis remonté dans la feuille `Synthèse`.

---

## La consolidation (`Ajouter1`) et le tableau croisé dynamique (`TCD`)

Pour analyser les 5 référentiels **ensemble**, les tableaux sont empilés en une
seule table via **Power Query**.

- **`Ajouter1`** est la table consolidée : elle reprend les mêmes colonnes que
  les référentiels, plus une colonne **`Tag`** qui indique de quel référentiel
  vient chaque ligne (`ANSSI - Hygiène`, `ANSSI - Admin`, `ISO 27001-2022`,
  `CIS v8`, `RGPD`). Cette feuille est **générée par la requête** : elle ne se
  modifie pas à la main, on modifie les feuilles de référentiel source.
- **`TCD`** est un tableau croisé dynamique basé sur `Ajouter1`. Il permet de
  croiser librement les données : par exemple `Tag` (référentiel) en lignes,
  `Niveau de mise en œuvre` en colonnes, un décompte en valeurs, et un filtre
  sur `Périmètre`.

### ⚠️ Important : l'actualisation n'est pas automatique

La table `Ajouter1` et le `TCD` sont des **instantanés** : ils ne reflètent pas
les dernières saisies tant qu'on ne les **actualise** pas.

Après avoir modifié un référentiel :

1. Onglet **Données ▸ Actualiser tout** (met à jour la requête *et* le TCD).
2. Ou, pour automatiser : **Données ▸ Requêtes et connexions**, clic droit sur
   la requête ▸ **Propriétés** ▸ cocher **Actualiser les données lors de
   l'ouverture du fichier**.

À l'inverse, la feuille `Synthèse` (à base de formules) se met à jour
**immédiatement**, sans actualisation.

---

## Utilisation pas à pas

1. **Ouvrir** le classeur dans Excel (ou un tableur compatible gérant les
   tableaux structurés, les listes déroulantes, les formules `COUNTIFS`, et —
   pour la consolidation — Power Query et les tableaux croisés dynamiques).
2. **Choisir la ou les feuilles** de référentiel pertinentes pour votre
   périmètre.
3. Pour chaque ligne, renseigner :
   - le **Périmètre** (via la liste déroulante) ;
   - le **Niveau de mise en œuvre** (via la liste déroulante) ;
   - le **Plan d'action / Commentaires** et, si besoin, la **Justification**.
4. La feuille **`Synthèse`** se met à jour automatiquement.
5. Faire **Données ▸ Actualiser tout** pour mettre à jour la consolidation
   `Ajouter1` et le `TCD`.
6. Analyser dans `TCD` (croisements par référentiel, statut, périmètre…).

> 💡 **Astuce** : commencez par qualifier le **périmètre** de tous les
> contrôles (Retenue / Exclue / n.a.) avant d'évaluer le niveau de mise en
> œuvre. Le taux n'a de sens qu'une fois le périmètre défini.

---

## Bonnes pratiques

- Ne saisir que dans les **feuilles de référentiel** : `Synthèse`, `Ajouter1`
  et `TCD` sont alimentées automatiquement.
- Ne pas casser les **tableaux structurés** : ajouter des lignes via le tableau
  lui-même pour que les formules et la requête restent valides.
- Utiliser systématiquement les **listes déroulantes** : les libellés exacts
  conditionnent le bon comptage.
- Penser à **Actualiser tout** (ou activer l'actualisation à l'ouverture) pour
  que le TCD reflète les dernières saisies.
- **Dater** chaque campagne d'évaluation (ex. copie du fichier par exercice)
  pour suivre la progression dans le temps.
- Vérifier les **intitulés officiels** des référentiels marqués ⚠️ avant tout
  usage en audit formel.

---

## Prérequis

- Microsoft Excel (recommandé) prenant en charge : tableaux structurés,
  validation de données (listes), fonctions `COUNTIF` / `COUNTIFS` / `SUM` /
  `ROUND` / `IFERROR`, **Power Query** et **tableaux croisés dynamiques**.
- Les fonctionnalités Power Query et TCD peuvent être limitées ou absentes dans
  certains tableurs alternatifs.

---

## Avertissement

Ce classeur est un **outil d'auto-évaluation** destiné à faciliter le pilotage
interne. Il ne constitue pas une certification ni un avis de conformité. Les
intitulés des contrôles doivent être confrontés aux publications officielles
des référentiels concernés (ANSSI, ISO/IEC, CIS) et au texte du RGPD.
