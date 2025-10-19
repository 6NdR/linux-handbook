## Daemon *cron*

***Définiton***

Le daemon *cron* est un service qui permet de programmer et d'automatiser des tâches d'administration sur le système par l'intermédiaire de tables appelées *crontab*.


***Commandes***

| Commandes | Fonctions | Options | Commentaires |
| :-------: |:---------:|:-------:|:------------:|
| *crontab* | Permet de gérer les tâches planifiées (cron jobs) sur le système | [Manuel : crontab](https://www.ibm.com/docs/fr/aix/7.3?topic=c-crontab-command)<br>*-e* : éditer le fichier crontab<br>*-l* : lister les jobs du fichier crontab de l'utilisateur<br>*-r* : supprimer les jobs du fichier crontab de l'utilisateur<br>*-u* : préciser un utilisateur<br>*-v* : affiche le status des jobs définis dans le fichier crontab de l'utilisateur | - |


***Commandes utiles***

```console
Lister les tâches du fichier crontab d'un utilisateur :
crontab -l
crontab -l -u <user>

Editer les tâches du fichier crontab d'un utilisateur :
crontab -e
crontab -e -u <user>

Supprimer les tâches du fichier crontab d'un utilisateur
crontab -r
crontab -r -u <user>
```

## Fichiers et répertoires

| Fichiers | Détails | Commentaires |
| :------: |:-------:| :----------: |
| */etc/crontab* | Fichier crontab principal pour la configuration de tâches systèmes | - |
| */etc/cron.hourly/* | Répertoire contenant les fichiers crontab pour la configuration de tâches systèmes horaires | - |
| */etc/cron.daily/* | Répertoire contenant les fichiers crontab pour la configuration de tâches systèmes quotidiennes | - |
| */etc/cron.weekly/* | Répertoire contenant les fichiers crontab pour la configuration de tâches systèmes hebdomadaire | - |
| */etc/cron.monthly/* | Répertoire contenant les fichiers crontab pour la configuration de tâches systèmes mensuelles | - |
| */etc/cron.yearly/* | Répertoire contenant les fichiers crontab pour la configuration de tâches systèmes annuelles | - |
| */etc/cron.d/* | Répertoire contenant les fichiers crontab pour la configuration de tâches systèmes supplémentaires et réccurentes | - |
| */var/spool/cron/crontabs/<br>var/spool/cron/* | Répertoires contenant les fichiers crontab pour la configuration des tâches des utilisateurs | Ne pas éditer directement ces fichiers : passer par la commande *crontab* |
| */var/log/cron.log* | Fichier de log associé au daemon *cron* | - |
| */etc/cron.allow*<br>*/etc/cron.deny* | Fichiers permettant de gérer les autorisations de l'utilisation de la commande *crontab* | Si **/etc/cron.allow** existe, alors le fichier */etc/cron.deny* est ignoré. Seuls les utilisateurs qui sont spécifiquement listés dans le fichier */etc/cron.allow* peuvent alors utiliser la commande *crontab* pour créer et gérer leurs propres tâches *cron*.<br>Si */etc/cron.allow* n'existe pas et que **/etc/cron.deny** existe, alors le système se réfère aux utilisateurs qui sont spécifiquement listés dans le fichier */etc/cron.deny* pour restreindre l'accès à la commande *crontab*.<br>Si **aucun des fichiers */etc/cron.allow* et */etc/cron.deny* n'existe**, alors tous les utilisateurs peuvent planifier des tâches avec *crontab*, sauf restrictions spécifiques définies ailleurs sur le système.|


## Syntaxe *crontab*

```
Définition d'une tâche dans un fichier crontab système :
# .---------------- Minute (0 - 59)
# |  .------------- Heure (0 - 23)
# |  |  .---------- Jour du mois (1 - 31)
# |  |  |  .------- Mois (1 - 12) ou (jan, feb, mar, ..., dec)
# |  |  |  |  .---- Jour de la semaine (0 - 6 ; sunday=0 ou 7) ou (sun, mon, tue, ..., sat)
# |  |  |  |  |
# *  *  *  *  *  username commande

Définition d'une tâche dans un fichier crontab utilisateur :
# .---------------- Minute (0 - 59)
# |  .------------- Heure (0 - 23)
# |  |  .---------- Jour du mois (1 - 31)
# |  |  |  .------- Mois (1 - 12) ou (jan, feb, mar, ..., dec)
# |  |  |  |  .---- Jour de la semaine (0 - 6 ; sunday=0 ou 7) ou (sun, mon, tue, ..., sat)
# |  |  |  |  |
# *  *  *  *  *  commande
```

| Valeurs | Effets |
| :-----: |:------:|
| * | Toutes les valeurs |
| , | Séparateur de liste de valeurs |
| - | Séparateur de gamme de valeurs |
| / | Séparateur de saut de valeurs |
| @yearly | Tous les ans |
| @annually | Tous les ans |
| @monthly | Tous les mois |
| @weekly | Toutes les semaines |
| @daily | Tous les jours |
| @hourly | Toutes les heures |
| @midnight | Tous les jours à minuit |
| @reboot | Au boot de la machine |

[Crontab Guru : générateur de crontab](https://crontab.guru/)

A ajouter :
- Inutile de relancer le deamon cron à chaque ajout d'un job
- Exemples !!!!!