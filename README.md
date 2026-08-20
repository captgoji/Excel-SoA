# Audit organisationnel — Grille d'auto-évaluation sécurité & conformité

Classeur Excel permettant de piloter un **audit
organisationnel de sécurité de l'information** sur la base de plusieurs
référentiels reconnus. Il sert à **positionner l'organisation** contrôle par
contrôle, à **suivre l'avancement** d'un plan d'action et à obtenir
automatiquement un **taux de couverture** global et par référentiel.

---

## À quoi ça sert

- **Faire un état des lieux** de la posture sécurité de l'organisation face à
  des référentiels de place (ANSSI, ISO, CIS) et à la réglementation (RGPD).
- **Prioriser** : identifier ce qui n'est pas commencé, ce qui pose problème et
  ce qui est déjà en place.
- **Suivre un plan d'action** dans le temps grâce à une colonne dédiée.
- **Communiquer** : la feuille de synthèse fournit un tableau de bord chiffré,
  réutilisable en comité de pilotage ou en rapport d'audit.

---

## Contenu du classeur

Le fichier contient **6 feuilles** : une feuille de synthèse et cinq
référentiels.

| Feuille | Référentiel | Nb de contrôles | Identifiants |
|---|---|---|---|
| `Synthèse` | Tableau de bord global (agrégé) | — | — |
| `ANSSI - Hygiène` | Guide d'hygiène informatique de l'ANSSI | 42 | `M1` … `M42` |
| `ANSSI - Admin` | Recommandations pour l'administration sécurisée des SI | 77 | `R1` … `R71` (+ variantes) |
| `ISO 27001-2022` | Mesures de l'Annexe A (ISO/IEC 27001:2022) | 93 | `A.5.x` … `A.8.x` |
| `CIS v8` | CIS Critical Security Controls v8 | 153 | `1.1` … `18.5` |
| `RGPD` | Obligations RGPD par article | ~23 | `Art.5` … `Conservation` |

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

À droite du tableau, un **bloc récapitulatif** (colonnes I à M) recompte
automatiquement les contrôles par périmètre et par statut, et calcule le taux
de couverture de la feuille. **Ce bloc est calculé : ne pas le modifier à la
main.**

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

## Avertissement

Ce classeur est un **outil d'auto-évaluation** destiné à faciliter le pilotage
interne. Il ne constitue pas une certification ni un avis de conformité. Les
intitulés des contrôles doivent être confrontés aux publications officielles
des référentiels concernés (ANSSI, ISO/IEC, CIS) et au texte du RGPD.
