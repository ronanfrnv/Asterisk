Compte rendu GitHub - Configuration des répertoires d'Asterisk
Résumé
Ce compte rendu documente la configuration des répertoires d'Asterisk en se basant sur les informations fournies dans le fichier /etc/asterisk/asterisk.conf.

Configuration des répertoires
Dans le fichier asterisk.conf, les répertoires sont configurés sous la section [directories]. Voici la liste des répertoires et leurs chemins associés :

Répertoire de cache Asterisk :

astcachedir => /var/cache/asterisk
Répertoire de configuration Asterisk :

astetcdir => /etc/asterisk
Répertoire de modules Asterisk :

astmoddir => /usr/lib/asterisk/modules
Répertoire de données Asterisk :

astvarlibdir => /var/lib/asterisk
astdbdir => /var/lib/asterisk
astkeydir => /var/lib/asterisk
astdatadir => /var/lib/asterisk
astagidir => /var/lib/asterisk/agi-bin
Répertoire de files d'attente Asterisk :

astspooldir => /var/spool/asterisk
Répertoire d'exécution Asterisk :

astrundir => /var/run/asterisk
Répertoire de journaux Asterisk :

astlogdir => /var/log/asterisk
Répertoire d'exécutables Asterisk :

astsbindir => /usr/sbin
Répertoire des sons
Les sons d'Asterisk sont stockés dans le répertoire :

/var/lib/asterisk/sounds
Les sous-répertoires contenant les sons dans différentes langues sont organisés selon le format /<langue>/, par exemple /en/ pour les sons en anglais.

Si besoin d'installer les sounds Francais 

Aller dans le répertoire d'installation de Asterisk dans mon cas /root/asterisk
``` make menuselect ```
Attention bien penser à ouvrir en grand
Aller dans `Extra Sound Package`
Puis Séléctionner `Extra Sond FR GSM`
Puis sauvegarder et taper les deux commandes suivantes `MAKE` et `MAKE INSTALL`

Pour voir la version `asterisk -V`

####Accéder à la CLI 
Dans /etc/asterisk
```asterisk –rvvv```

Si vous remarquez des plantages et que vous voulez avoir un fichier de trace en sortie, utilisez la 
commande suivante : `asterisk –vvvvvvvvvc | tee /tmp/debug.log` et pour afficher 
le fichier log 
`tail –F /tmp/debug.log. `
