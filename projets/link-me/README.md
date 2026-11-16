# Link Me

> Une app Mac native pour décrocher un stage : elle trouve des contacts LinkedIn, déduit leur e-mail pro, envoie des candidatures personnalisées et suit chaque piste.

**Type** : app Mac (projet à deux) · **Techno** : Swift, SwiftUI (Liquid Glass, macOS 26), Supabase, API Claude · **Statut** : les 5 étapes du cahier des charges sont livrées (v0.1.10) · **Période** : octobre 2026

![Suivi des candidatures : chiffres clés et colonnes de « À contacter » à « Offre » et « Refus »](images/01-suivi.png)

## Le problème
Chercher un stage par candidatures spontanées, c'est trouver la bonne personne, deviner son e-mail, écrire, relancer et suivre les réponses. Nous étions deux à chercher en même temps, au risque d'écrire chacun à la même personne.

## Ce que fait l'outil
- **Contacts LinkedIn** : l'app relève les profils dans une vue intégrée, sous des plafonds prudents, et s'arrête au moindre CAPTCHA .
- **Adresses e-mail** : formats probables vérifiés par Hunter puis Dropcontact, avec niveau de confiance.
- **Campagnes** : accroche proposée par Claude et toujours relue, envoi depuis ma propre adresse sous plafond quotidien.
- **Relances et suivi** : relances annulées dès qu'une réponse arrive, colonnes de « À contacter » à « Offre ».
- **Registre commun** (Supabase) : il prévient d'un doublon et bloque l'envoi à une personne contactée par l'autre dans les 6 derniers mois.

## En images
| | |
|---|---|
| ![](images/02-adresses.png) | ![](images/03-campagnes.png) |
| Adresses e-mail et niveau de confiance | Campagne : chaque mail est relu, programmé puis suivi |

![](images/04-registre.png)
Registre commun : qui a écrit à qui, et où en est la piste

Toutes les captures viennent du mode démo de l'app, avec des données inventées.

## Comment je l'ai construit
Projet mené à deux, dont les 13 commits du dépôt viennent de mon compte. Je l'ai construit avec Claude Code : j'ai écrit le cahier des charges, il a écrit le code, j'ai vérifié chaque étape sur de vrais cas. Un choix de prudence : pas de sondage des serveurs mail pour vérifier une adresse (technique associée au spam). Au total, environ 12 000 lignes de Swift, aucune dépendance externe et 368 vérifications automatiques.

Code privé, démo possible sur demande.
