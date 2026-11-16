# StreamFlix

> Mon Netflix personnel : une app Mac, Windows et iPhone qui présente et lit ma vidéothèque Jellyfin.

**Type** : app Mac et Windows, web app iPhone et iPad · **Techno** : React, TypeScript, Tauri, Jellyfin · **Statut** : terminé, utilisé chez moi · **Période** : novembre 2026

![L'accueil : le film à la une avec son heure de fin, puis les rangées, à commencer par « Reprendre la lecture »](images/01-accueil.png)

## Le problème
Jellyfin classe et diffuse très bien, mais son interface n'a pas la mise en scène de Netflix. Je voulais ce confort sur Mac et iPhone, avec ce que Netflix ne fait pas : dire à quelle heure le film finira et garder la trace de ce que j'ai vu.

## Ce que fait l'outil
- **Un accueil à la Netflix** : des films à la une, puis des rangées qui disent pourquoi elles sont là (reprise, Top 10, récents, genres).
- **Une app qui connaît l'heure** : chaque film affiche « Finit à 23:12 » ; l'écran *Ce soir* propose ceux qui tiennent avant l'heure choisie.
- **Fiche, lecteur et recherche ⌘K** : fiche technique, reprise là où on s'était arrêté, fautes de frappe tolérées.
- **Le Carnet** : chaque film vu s'y inscrit avec mon avis, identique sur le Mac et l'iPhone.

## En images
| | |
|---|---|
| ![](images/02-fiche.png) | ![](images/03-rangees.png) |
| La fiche d'un film. | Les rangées et le Top 10. |

![](images/04-iphone.png)

*Sur iPhone.*

Captures de la vraie interface, avec un catalogue fictif et un serveur Jellyfin simulé.

## Comment je l'ai construit
Construit avec Claude Code : je décris le besoin et les règles, Claude Code écrit le code, je vérifie. Avant la première ligne, un plan de 31 pages fixait la vision et 14 maquettes. Le choix principal : ne refaire aucune fonction de Jellyfin et ne construire que l'interface, avec une seule base React pour le Mac (fenêtre Tauri), Windows et l'iPhone ; même le Carnet n'a pas de serveur à lui. L'ensemble fait un peu plus de 3 000 lignes de TypeScript, avec 28 tests automatiques. Leçon : plan et maquettes d'abord donnent à chaque étape une cible précise à vérifier.

Code privé, démo possible sur demande.
