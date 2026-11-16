# Export automatique des relevés

> Des scripts Mac qui pilotent l'extranet d'une plateforme de gestion pour en sortir seuls les 7 relevés qui alimentent le logiciel d'un cabinet de gestion de patrimoine, en refusant tout fichier non conforme.

**Type** : scripts Mac à double-cliquer · **Techno** : Python (bibliothèque standard), JavaScript injecté dans Safari par les Apple Events, Electron pour les essais · **Statut** : terminé, utilisé sur le vrai extranet · **Période** : novembre 2026

![Schéma de la chaîne, de l'extranet aux rapports clients du cabinet](images/01-chaine.png)

## Le problème
Dans le cabinet de gestion de patrimoine où j'ai fait mon stage, les données des contrats (clients, supports, mouvements, plus-values) arrivent par une plateforme de gestion en ligne. Le logiciel du cabinet, qui produit notamment les rapports clients, se met à jour à partir de 7 fichiers Excel à sortir de cet extranet en suivant à la lettre un manuel d'import : requêtes, menus, cases à cocher, dates. Une case de trop décale toutes les colonnes, et l'erreur ne se voit qu'à l'import.

## Ce que fait l'outil
- Fait seul les 7 exports dans l'onglet Safari où l'utilisateur est déjà connecté (double authentification) : le script ne voit ni ne garde aucun identifiant.
- Ne reprend que les mouvements récents : depuis le dernier export, moins 92 jours pour les opérations saisies en retard. Un fichier par année, et le message « Aucun mouvement » de l'extranet est géré.
- Reconnaît chaque fichier téléchargé à ses colonnes, pas à son nom, et le compare au manuel : nombre de colonnes, titres, case en trop, période couverte. Un fichier faux est effacé aussitôt, avec la raison et la page du manuel.
- Range les 7 étapes dans un dossier daté, prêtes à déposer dans la page d'import du logiciel ; rien n'est copié tant qu'une étape est à refaire.
- Reprend là où il s'est arrêté et, en cas de blocage, dit à quelle étape et quoi faire. Il note les commandes de l'écran bloqué, jamais le contenu d'un tableau, pour corriger le script sans tout refaire.
- Un enregistreur, lancé une fois, note les clics de l'utilisateur (boutons, menus, cases, dates) en écartant noms, adresses mail et longs numéros.

## En images
| | |
|---|---|
| ![](images/02-execution.png) | ![](images/03-controle.png) |
| Exécution réelle du script sur un faux extranet, données inventées (sortie du terminal mise en page, noms neutralisés) | Exécution réelle du contrôle sur des fichiers fictifs : trois exports refusés, chacun avec sa raison |

![](images/04-extrait.png)
*Extrait commenté : un geste joué dans la page (les cases trouvées par leur libellé) et l'étape qui l'enchaîne avec le contrôle du fichier.*

## Comment je l'ai construit
Construit avec Claude Code en une semaine : je décrivais le besoin et les règles, Claude Code écrivait le code, je vérifiais chaque résultat sur le vrai extranet. Pour que l'IA ne voie jamais de données de clients, on a procédé en « je clique, tu enregistres » : j'ai fait les 7 exports une fois à la main pendant que l'enregistreur notait la seule structure des écrans, et le script d'export a été écrit à partir de ce relevé. Une première version dans une fenêtre de navigateur à part a été abandonnée : avec la double authentification, seul mon Safari était connecté, d'où le pilotage de Safari par les Apple Events.

Le premier passage réel a buté sur des détails que seul le vrai site montre : liste des requêtes sur quatre pages, message au lieu d'un fichier vide, cases cachées derrière leur libellé, deux choix presque identiques dans une liste. Le contrôle des fichiers a refusé les deux derniers avant tout import. Résultat : les 7 exports faits seuls, environ 140 000 mouvements sur vingt ans en 21 fichiers, importés sans erreur ; depuis, une mise à jour ne reprend que les derniers mois. L'outil compte environ 1 250 lignes, plus 650 lignes d'essais (près de 60 vérifications) qui rejouent tout sur un faux extranet sans toucher au vrai.

Ce que j'en retiens vaut pour tout travail sur l'extranet d'un assureur ou d'une plateforme, comme celui que fait l'agent de Charlie : un clic qui réussit ne prouve rien, c'est le fichier obtenu qu'il faut vérifier, et le script doit savoir s'arrêter en disant pourquoi.

Code privé (outil d'un cabinet), démo possible sur demande.
