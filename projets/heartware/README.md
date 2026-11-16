# Heartware

> Un utilitaire d'entretien natif pour macOS, gratuit : nettoyage, sécurité, applications, stockage et menu d'état réunis dans une seule app.

**Type** : app Mac native · **Techno** : Swift, SwiftUI, Swift Package Manager · **Statut** : en cours, versions publiées sur GitHub · **Période** : octobre 2026

![Le tableau de bord de Heartware : note de santé du Mac, analyse intelligente, activité en direct et conseils](images/01-tableau-de-bord.png)

## Le problème
Pour garder un Mac propre et sûr, on jongle entre plusieurs utilitaires, souvent payants, et on hésite à les laisser supprimer des fichiers sans savoir lesquels. Je voulais une app gratuite qui explique ce qu'elle trouve et ne supprime rien sans accord.

## Ce que fait l'outil
- **Tableau de bord** : une note de santé sur 100 et des conseils classés par utilité.
- **Nettoyage** : caches, journaux, outils de développement ; tout passe par une confirmation, et rien n'est effacé directement.
- **Sécurité** : un bilan de 40 points avec correction en un clic, et un antimalware qui applique les 572 règles d'Apple (XProtect).
- **Applications et stockage** : désinstallation complète, carte du disque.
- **Menu d'état, lanceur et assistant Claude** : suivi du Mac dans la barre des menus, `⌥ Espace` pour tout lancer, et un assistant qui répond en français.

## En images
| | |
|---|---|
| ![](images/02-nettoyage.png) | ![](images/03-protection.png) |
| Le nettoyage : on coche ce qui part | Le bilan de sécurité |
| ![](images/04-stockage.png) | |
| La carte du disque | |

Captures du mode démo, avec un Mac et un utilisateur inventés.

## Comment je l'ai construit
Je l'ai construit avec Claude Code : je décris le besoin et les règles, il écrit le code, je vérifie chaque résultat sur mon Mac. Les règles sont écrites une fois dans un fichier relu à chaque session : toute suppression passe par un seul point d'entrée qui refuse ce qui sort du dossier personnel. Le résultat fait environ 103 000 lignes de Swift sans aucune dépendance, avec plus de 40 versions publiées. J'en retiens que, pour un outil qui supprime des fichiers, les garde-fous comptent plus que les fonctions : « un nettoyeur qui supprime trop, c'est pire que pas de nettoyeur ».

**Code source** : https://github.com/Olima34/Heartware
