# Vigie

> Une aide à la décision qui tourne sur mon Mac pour le concours de gestion de portefeuille Next Challenge 2026-2027 : elle analyse et prépare, je décide et je passe les ordres moi-même.

**Type** : app Mac (Electron) avec interface web locale · **Techno** : Python, SQLite, Electron, Claude Code · **Statut** : utilisé au quotidien pendant le concours · **Période** : octobre 2026

![Écran « Aujourd'hui » : valeur du portefeuille, conformité aux règles, tâches à traiter et agenda du concours](images/01-aujourdhui.png)

## Le problème
Le Next Challenge (plateforme NextWise) confie à chaque étudiant 50 000 € virtuels à gérer d'octobre à avril sur sept places Euronext, avec des règles de diversification (au moins 10 actions et 4 secteurs, aucune ligne au-dessus de 15 %) et un barème non publié. Suivre seul chaque jour des centaines de titres, les règles et l'actualité n'est pas tenable. Le règlement (article 7) autorise l'IA pour analyser et contester une idée, mais interdit tout programme qui agit sur la plateforme.

## Ce que fait l'outil
- Collecte chaque jour cours, fondamentaux, estimations d'analystes, actualités et indicateurs macro, et rattrape seul les mises à jour manquées pendant que le Mac dormait.
- Note chaque action face à son industrie (tendance, révisions de bénéfices, qualité, risque) et propose chaque semaine un rééquilibrage, avec le portefeuille avant et après.
- Contrôle la conformité aux règles du concours, y compris ce qu'elle deviendra si les ordres en attente s'exécutent.
- Rédige une fiche de décision par ordre proposé : thèse, signaux chiffrés, risques, critères de sortie et sources datées.
- Fait travailler Claude en lecture seule : veille de l'actualité avec mémoire, note macro, critique de la proposition ; chaque réponse liste ses sources.
- Prévient par notification : ordre probablement exécuté, mouvement inhabituel, résultats publiés par une société détenue.

## L'outil prépare, je décide
Vigie ne se connecte jamais à NextWise : aucun identifiant stocké, aucune collecte, aucun ordre passé à ma place. Je passe chaque ordre à la main, puis je le saisis dans Vigie. Une fiche de décision ne se valide qu'après avoir coché « J'ai lu et compris » et reformulé la décision en une phrase, avec mes mots. Claude ne reçoit aucun outil d'écriture, et une règle de permission (vérifiée par un test) lui interdit d'ouvrir les pages NextWise. Enfin, aucun chiffre n'est inventé : une donnée absente s'affiche « n.d. », et la proposition est bloquée si les cours sont périmés.

## En images
| | |
|---|---|
| ![](images/02-proposition.png) | ![](images/03-fiche.png) |
| Proposition de la semaine : avant/après et ordres proposés, chacun avec sa fiche | Fiche de décision : risques, sortie, sources, puis ma décision avec mes mots |

![Tableau de bord : régime de marché, mode de pilotage et indicateurs macro avec leurs seuils](images/04-tableau.png)
*Tableau de bord : régime de marché, mode de pilotage et indicateurs macro, chacun avec sa courbe sur un an et ses seuils.*

## Comment je l'ai construit
Je l'ai construit avec Claude Code. J'ai commencé par un cahier des charges complet : règles du concours vérifiées, stratégie, garde-fous non négociables, lots de livraison avec critères d'acceptation. Claude Code a ensuite écrit le code lot par lot, et je vérifiais chaque résultat sur de vrais cas : mes ordres réels, les liquidités affichées par la plateforme, les classements publiés. Le projet compte environ 12 300 lignes de Python, 2 400 lignes d'interface et 1 300 pour l'app Mac, avec 120 tests qui tournent sans réseau sur des réponses réelles enregistrées. Deux choix m'ont appris le plus : recaler le barème inconnu à partir des points que je saisis à chaque classement, et faire travailler Claude par mon abonnement, sans clé d'API obligatoire et sans aucun droit d'agir. Au classement du Transac' Challenge du 30 octobre 2026, le portefeuille était 1er sur 103 participants.

Code privé, démo possible sur demande.
