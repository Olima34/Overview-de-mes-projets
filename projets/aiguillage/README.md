# Aiguillage

> Pour chaque tâche confiée à Claude Code, Aiguillage choisit le modèle et la puissance qui suffisent, dit pourquoi en une phrase, puis lance Claude Code avec ce choix.

**Type** : app Mac et outil en ligne de commande · **Techno** : TypeScript, Electron + React, Qwen3.6 en local (MLX) · **Statut** : prototype · **Période** : novembre 2026

![L'écran Nouvelle tâche : la tâche est triée, Aiguillage choisit Sonnet 5.5 en low et explique pourquoi](images/01-tache.png)

## Le problème
Claude Code laisse choisir le modèle (Haiku, Sonnet, Opus, Fable) et la puissance de réflexion, de low à max. Par habitude, je mettais presque tout au maximum : dans mon historique de juillet à novembre 2026 (1 665 demandes), 91 % étaient parties en xhigh ou max, alors qu'Anthropic conseille de partir d'Opus en medium et de monter seulement si besoin. Je voulais savoir ce que ça coûtait vraiment, et un outil qui fasse le bon choix à chaque tâche.

## Ce que fait l'outil
- **Trie la tâche** : son type (débogage, refonte, rédaction…) et sa difficulté sur 10, avec Qwen3.6 qui tourne sur le Mac (environ 0,45 s, le texte ne sort pas pour choisir), ou avec le classifieur de Fil, instantané, quand Qwen n'est pas chargé.
- **Choisit le réglage** : il part du défaut d'Anthropic (Opus 5.5 en medium), monte sur une tâche difficile, ne descend que sur une tâche simple hors code. Le routeur compare la chance de réussir du premier coup au coût estimé du tour.
- **Explique le choix** en une phrase et montre les options écartées, avec leur chance de réussite et leur coût. On peut en prendre une autre avant de lancer.
- **Lance Claude Code** dans un terminal intégré à l'app, avec `--model` et `--effort` : un seul choix par session, pour ne pas perdre le cache.
- **Garde un journal** de chaque choix sur le Mac, et **rejoue l'historique** Claude Code pour chiffrer ce que ces choix auraient économisé.

## En images
| | |
|---|---|
| ![](images/02-direct.png) | ![](images/03-economies.png) |
| En direct : une demande d'exemple traverse l'arbre de décision du vrai moteur. | Économies : mon historique rejoué, réglages simples contre Aiguillage. |

![](images/04-journal.png)
*Journal : chaque choix tracé, avec l'écart de coût face à mon réglage habituel (tâches d'exemple).*

## Ce que disent les mesures
Mes 1 665 demandes rejouées une à une, tri par Qwen, face à mon habitude (83 % de réussite estimée sur les 560 tâches difficiles) :
- **Le gros du gain tient dans un réglage** : Opus en medium partout, le défaut d'Anthropic, coûte 33,7 % de moins, mais tombe à 75 % sur les tâches difficiles.
- **Aiguillage, un choix par session** (ce que fait le lanceur) : −32,6 % et 76 % sur le difficile. Il fait jeu égal avec ce défaut, pas mieux.
- **Aiguillage, un choix revu à chaque demande** : le même −32,6 %, mais 82 % sur le difficile, presque la qualité de mon habitude. C'est la suite à construire.
- **Le tri** : sur 36 vrais messages, Qwen trouve le bon type de tâche dans 56 % des cas, contre 39 % pour le classifieur de Fil (91 % sur 240 exemples de test).
- **Qwen ne remplace pas Claude** : sur 33 vraies demandes jugées à l'aveugle par Claude, sa réponse suffisait dans 42 % des cas, celle de Claude dans 100 %. Il trie, il ne fait pas le travail.

Limites : les réussites sont estimées par un modèle calé sur des benchmarks publics, pas observées, et il n'y a qu'un historique, le mien.

## Comment je l'ai construit
Je l'ai construit en un week-end avec Claude Code : je décris le besoin et les règles, Claude Code écrit le code, je vérifie chaque résultat sur de vrais cas. Le cœur (le tri, le routeur, le catalogue des modèles) vient de Fil, mon assistant qui choisit déjà entre plusieurs IA et qui a sa propre fiche ; Aiguillage l'applique à Claude Code. Une contrainte a tout décidé : un hook de Claude Code ne peut pas changer de modèle, donc le choix se fait au lancement. La mesure m'a corrigé plusieurs fois : mon premier chiffre comparait à mon habitude au lieu du défaut d'Anthropic, et mon rejeu oubliait que changer de puissance en cours de session fait perdre le cache. J'en retiens qu'il faut mesurer avant d'affirmer, et garder les chiffres qui ne m'arrangent pas. Environ 5 800 lignes de TypeScript, dont la moitié pour le cœur repris de Fil, et 93 tests. L'interface reprend la direction artistique de Charlie.

Code privé, démo possible sur demande.
