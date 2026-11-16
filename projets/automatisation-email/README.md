# Prospection par e-mail automatisée

> Une petite application web pour envoyer des e-mails de prospection à partir de modèles, personnalisés avec le prénom du destinataire et relus dans un aperçu.

**Type** : application web · **Techno** : React, TypeScript, Tailwind CSS, API SendGrid · **Statut** : prototype · **Période** : juin 2025

![L'écran principal : destinataire, choix du modèle et aperçu de l'e-mail personnalisé (données fictives)](images/01-accueil.png)

## Le problème
En prospection, on envoie sans cesse les mêmes messages en changeant quelques éléments. Les recopier prend du temps et expose aux erreurs : mauvais prénom, adresse mal saisie, mauvais message.

## Ce que fait l'outil
- Propose 4 modèles : introduction, suivi, proposition, invitation.
- Insère le prénom du destinataire et affiche en direct l'aperçu exact : destinataire, objet et corps.
- Bloque l'envoi tant que le prénom manque ou que l'adresse est invalide, en disant quoi corriger.
- Envoie par l'API SendGrid, puis confirme ou affiche l'erreur.

## En images
| | |
|---|---|
| ![](images/02-modeles.png) | ![](images/03-controle.png) |
| Un autre modèle : l'aperçu suit | Adresse invalide : le bouton d'envoi reste grisé |

![](images/04-envoi.png)

*La confirmation après l'envoi (envoi simulé : aucun e-mail n'est parti).*

Toutes les captures utilisent des données fictives.

## Comment je l'ai construit
C'est mon projet le plus simple, fait en une journée (5 juin 2025), et il n'a pas été construit avec Claude Code. La première version de l'interface a été déposée d'un bloc sur GitHub, puis j'ai confié les évolutions à Codex, l'agent de code d'OpenAI, en 8 pull requests . Environ 550 lignes en tout. La limite principale est claire : l'appel à SendGrid part directement du navigateur, donc la clé d'API se retrouve dans le code chargé par la page. C'est acceptable pour un essai en local, pas pour un vrai usage : il faudrait un petit serveur qui garde la clé.

**Code source** : https://github.com/Olima34/Automatisation-email
