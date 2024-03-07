**Compte rendu : Configuration des répertoires d'Asterisk**

Ce compte rendu documente la configuration des répertoires d'Asterisk en se basant sur les informations fournies dans le fichier `/etc/asterisk/asterisk.conf`.

**Configuration des répertoires :**

Dans le fichier `asterisk.conf`, les répertoires sont configurés sous la section `[directories]`. Voici la liste des répertoires et leurs chemins associés :

1. **Répertoire de cache Asterisk :**
   - `astcachedir` => `/var/cache/asterisk`

2. **Répertoire de configuration Asterisk :**
   - `astetcdir` => `/etc/asterisk`

3. **Répertoire de modules Asterisk :**
   - `astmoddir` => `/usr/lib/asterisk/modules`

4. **Répertoire de données Asterisk :**
   - `astvarlibdir` => `/var/lib/asterisk`
   - `astdbdir` => `/var/lib/asterisk`
   - `astkeydir` => `/var/lib/asterisk`
   - `astdatadir` => `/var/lib/asterisk`
   - `astagidir` => `/var/lib/asterisk/agi-bin`

5. **Répertoire de files d'attente Asterisk :**
   - `astspooldir` => `/var/spool/asterisk`

6. **Répertoire d'exécution Asterisk :**
   - `astrundir` => `/var/run/asterisk`

7. **Répertoire de journaux Asterisk :**
   - `astlogdir` => `/var/log/asterisk`

8. **Répertoire d'exécutables Asterisk :**
   - `astsbindir` => `/usr/sbin`

9. **Répertoire des sons :**
   - Les sons d'Asterisk sont stockés dans le répertoire `/var/lib/asterisk/sounds`.
   - Les sous-répertoires contenant les sons dans différentes langues sont organisés selon le format `/<langue>/`, par exemple `/en/` pour les sons en anglais.

**Installation des sons français :**

Pour installer les sons français, procédez comme suit :

1. Accédez au répertoire d'installation d'Asterisk, par exemple `/root/asterisk`.
2. Utilisez la commande `make menuselect`.
3. Ouvrez "Extra Sound Package".
4. Sélectionnez "Extra Sound FR GSM".
5. Sauvegardez et tapez les commandes `MAKE` et `MAKE INSTALL`.

**Vérification de la version d'Asterisk :**

Pour voir la version d'Asterisk, utilisez la commande `asterisk -V`.

**Accès à la CLI :**

Pour accéder à l'interface de ligne de commande (CLI), utilisez la commande `asterisk –rvvv` depuis le répertoire `/etc/asterisk`.

Si vous rencontrez des plantages et souhaitez obtenir un fichier de trace en sortie, utilisez la commande suivante : `asterisk –vvvvvvvvvc | tee /tmp/debug.log`, et pour afficher le fichier journal, utilisez `tail –F /tmp/debug.log`.
Pour sortir de la console tapez la commande `exit`.

Si vous avez modifié le fichier sip.conf, il vous suffira dans la CLI de taper la commande sip 
reload.

Si vous avez modifié le fichier sip.conf, il vous suffira dans la CLI de taper la commande `sip reload`. 
Si vous avez modifié le fichier extensions.conf (plan de numérotation), , il vous suffira dans 
la CLI de taper la commande `dialplan reload`. 
Pour recharger presque la totalité des configurations d'asterisk il suffit de taper la commander 
`reload`. 

**Fichier SIP.conf***
Le fichier d'Asterisk qui permet d'enregistrer les différents téléphones SIP s'appelle sip.conf et il 
se trouve dans /etc/asterisk/sip.conf. 
Avant toutes choses vérifiez que vous avez bien sauvegardé (renommé) votre fichier sip.conf en 
sip.conf.bak ou en sip.conf.old. 
Puis tapez la commande :
 : echo "" > /etc/asterisk/sip.conf. 
 
Ce fichier contient plusieurs sections séparées par des crochets. Ouvrez le fichier d'exemples 
original et donner le nom de la première section.
Dans notre cas :  `[general]`

La section `[general]` dans la configuration d'Asterisk est une section globale qui définit des paramètres généraux pour le fonctionnement global du système Asterisk. Cette section est souvent utilisée pour définir des paramètres qui affectent le comportement global du serveur Asterisk, tels que les paramètres de journalisation, les paramètres réseau, les paramètres de sécurité, etc.

Voici quelques exemples de ce que vous pourriez trouver dans une section `[general]` dans la configuration d'Asterisk :

Paramètres de journalisation: Vous pouvez spécifier le niveau de détail des journaux système et leur emplacement.

Paramètres réseau: Vous pouvez spécifier les interfaces réseau à utiliser, les ports d'écoute, les protocoles pris en charge, etc.

Paramètres de sécurité: Vous pouvez configurer des options de sécurité telles que le chiffrement des communications, les autorisations d'accès, etc.

Paramètres de performance: Vous pouvez ajuster les paramètres liés aux performances du système, tels que le nombre maximal de connexions simultanées, les tampons de mémoire, etc.

Paramètres de localisation: Vous pouvez spécifier des paramètres de localisation, tels que le fuseau horaire par défaut, les paramètres régionaux, etc.

En résumé, la section `[general]` dans la configuration d'Asterisk sert à définir des paramètres globaux qui affectent le fonctionnement global du système.

Toutes les sections suivantes permettent de définir les téléphones sip. Il y en aura autant que de 
téléphones sip.

*** Création du fichier Général ***
Editer dans votre fichier sip.conf les lignes suivantes (le texte précédé d'un poit-virgule 
correspond aux commentaires, ce texte est donc facultatif) 

Le fichier sip.conf est un élément essentiel dans la configuration d'un serveur Asterisk, qui gère les paramètres liés aux connexions SIP (Session Initiation Protocol). Voici un compte rendu des éléments de la section [general] de ce fichier :

context=tata : Ce paramètre indique le contexte par défaut dans lequel les téléphones SIP définis ultérieurement dans le fichier seront placés. Cela permet de déterminer les règles de composition des numéros et les autorisations associées.

bindport=5060 : Il spécifie le port sur lequel le serveur Asterisk écoutera les requêtes SIP entrantes. Le port par défaut pour le protocole SIP est 5060.

bindaddr=0.0.0.0 : Cette adresse IP spécifie sur quelle interface le serveur va écouter le trafic SIP. La valeur 0.0.0.0 indique que le serveur écoutera sur toutes les interfaces disponibles.

srvlookup=yes : Ce paramètre autorise la résolution des noms DNS des appareils SIP, conformément à la RFC SIP.

disallow=all : Cette directive désactive tous les codecs par défaut.

allow=alaw : Il active le codec G.711 alaw, utilisé principalement aux États-Unis.

allow=gsm : Cela permet d'activer le codec GSM, qui est souvent utilisé pour les appels mobiles.

directmedia=no : Ce paramètre spécifie que le flux RTP (Real-time Transport Protocol), c'est-à-dire le flux vocal, ne passera pas directement entre les deux appareils téléphoniques sans passer par le serveur Asterisk.

language=fr : Il indique la langue par défaut à utiliser pour les sons fournis par Asterisk. Ici, c'est le français.

type=friend : Ce paramètre est utilisé pour identifier les types de connexion, en l'occurrence, pour des appels entrants et sortants. Le type "friend" est utilisé pour identifier à la fois les appels entrants (utilisateur) et sortants (équipement).
Copier coller la suite : 
```
[general] 
context = tata ; commentaires
bindport=5060 
bindaddr=0.0.0.0 
srvlookup=yes 
disallow=all 
allow=alaw 
allow=gsm 
directmedia=no 
language=fr 
type=friend 
```
A la suite du général Ajouter les postes : 
```
[201] 
host=dynamic 
username=201 
type=friend 
secret=201
```
Pour le poste 202

```
[202] 
host=dynamic 
username=202
type=friend 
secret=202
```
Une fois fait aller dans le CLI d'Asterisk => `asterisk -rvvvvv`
Puis `sip reload` et `sip show peers`
Pour l'instant, les tépéphones sip sont bien paramétrés dans le fichier sip.conf. Il va falloir 
maintenant, enregistrer ces trois téléphones auprès de l'IPBX Asterisk. 

*** Enregistrement des téléphones ***
Sur l'interface Web de l'ip du téléphone :

Enregistrer le téléphone  : 

![image](https://github.com/ronanfrnv/Asterisk/assets/65066876/4a2cdb1b-9c7e-4953-817c-de1d5b26de5c)
![image](https://github.com/ronanfrnv/Asterisk/assets/65066876/34a1f63b-9b89-4ee9-b10a-60f3d6eeb0a3)

Une fois connecté : 
![image](https://github.com/ronanfrnv/Asterisk/assets/65066876/ddc235f4-394c-4751-878e-dca3fa2d304f)



