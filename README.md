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

Stoppez le service Asterisk en tapant `Core stop now`. 
Relancer le service Asterisk `/etc/init.d/asterisk start`
Dans la CLI activez le debug sip en tapant `sip set debug on`
Voici le détail des trames Wireshark
![image](https://github.com/ronanfrnv/Asterisk/assets/65066876/f7de3531-a9b0-431b-bbbc-af66203d67a4)
Voici le détail trame Subscribe 
![image](https://github.com/ronanfrnv/Asterisk/assets/65066876/6ad7410f-0eb9-40b9-81ca-38bce69066ce)
Voici le détail trame  Register
![image](https://github.com/ronanfrnv/Asterisk/assets/65066876/e947c780-a497-4b90-8b86-c76b1d04cf27)
Voici le détail trame  200OK
![image](https://github.com/ronanfrnv/Asterisk/assets/65066876/4776cf96-ce93-4f4b-a42e-e2a8b3c1c0e7)

*** Fichier Extensions.conf ***

Ce fichier revêt une importance capitale, étant donné qu'il définit le schéma de numérotation pour Asterisk. À noter : à partir de la version 1.6, il existe une alternative à ce fichier de configuration, à savoir le fichier extension.ael ou le fichier extensions.lua, offrant une syntaxe plus structurée pour mettre en place le schéma de numérotation. Dans notre cas, nous optons pour l'utilisation du fichier extensions.conf. Pour une meilleure clarté, veuillez supprimer les fichiers extensions.ael et extensions.lua. Ensuite, veuillez sauvegarder le fichier extensions.conf original.

Puis sauvegardez le fichier extensions.conf original : 
cd /etc/asterisk 
cp extensions.conf extensions.conf.bak 
echo "" > extensions.conf ; vide le fichier

La constitution du fichier "extensions.conf" se déroule comme suit :
Le fichier commence par deux sections facultatives :

La section [general], destinée à définir les paramètres qui s'appliqueront à l'ensemble du fichier.
La section [globals], réservée à la définition des variables globales qui seront utilisées ultérieurement.
Ensuite, il nous revient de créer les sections suivantes, que nous nommerons dorénavant des "contextes". Un contexte est toujours défini entre crochets. La fin d'un contexte est signalée par le nom du contexte suivant.

Ensuite, il nous revient de constituer les sections ultérieures, que nous désignerons dorénavant sous le nom de "contextes". Chaque nom de contexte sera toujours encadré par des crochets. La fin d'un contexte sera signalée par le nom du contexte suivant.

Exemple :
```
[general]
Paramètres applicables dans l'ensemble du fichier
[globals]
Définition des variables globales
[context1]
Blabla...

```
Dans notre cas 
```
[general]
Paramètres applicables dans l'ensemble du fichier
[globals]
Définition des variables globales
[tata] 
exten => 201,1,Dial(SIP/201) 
exten => 202,1,Dial(SIP/202) 

```
Après avoir enregistré le fichier, allez dans la CLI est recharger le dialplan en tapant `dialplan 
reload`. 

Si on change les contexts par titi alors : 
![image](https://github.com/ronanfrnv/Asterisk/assets/65066876/2d4005f3-07e9-4ba0-a0c7-e61ee7407693)
La communication ne se fait pas voir messages d'erreur ci dessus

La commande pour afficher l'ensemble des téléhpones connectés `sip show peers`
![image](https://github.com/ronanfrnv/Asterisk/assets/65066876/344b9067-8717-4764-a9bc-2ba7723d54b2)

La commande pour afficher la config d'un téléhpone connecté `sip show peer 202`

![image](https://github.com/ronanfrnv/Asterisk/assets/65066876/ef865ba5-18bc-4d5d-bf03-1ff0e9977699)

La commande `sip show channels` :
Cette commande permet d'afficher des informations sur les canaux SIP actifs sur le système, y compris les canaux entrants et sortants.
![image](https://github.com/ronanfrnv/Asterisk/assets/65066876/5d08e7be-f7b2-4ea2-bda4-24a7ed4247f5)

Lorsqu'il n'y a pas de communications : 
![image](https://github.com/ronanfrnv/Asterisk/assets/65066876/66c0c656-19c5-4ab9-804e-99b0fb3d159c)

Lorsqu'il y a communications : 
![image](https://github.com/ronanfrnv/Asterisk/assets/65066876/5b5dc94e-cbaa-4bf2-9d62-87f21da60e74)

*** Configurer le temps de tonaliter ***
Dans le contexte [tata], vous allez modifier :
```
exten => 201,1,Dial(SIP/201) 
```
En : 
```
exten => 201,1,Dial(SIP/201,5) 
```
Puis par 10

```
exten => 201,1,Dial(SIP/201,10) 
```
Voici une explication détaillée de cette commande :

exten: C'est un mot-clé qui indique que cette ligne de configuration est associée à une extension spécifique dans le plan de numérotation.

201: C'est le numéro d'extension auquel cette ligne de configuration est associée. Dans ce cas, c'est l'extension 201. Lorsqu'un appel est dirigé vers cette extension, cette ligne de configuration sera exécutée.

1: C'est la priorité de l'action. Dans ce cas, la priorité est 1. Si plusieurs actions sont définies pour la même extension, elles seront exécutées dans l'ordre de priorité.

Dial(SIP/201,5): C'est l'action à effectuer lorsque cette extension est appelée. Cette action est un appel à la fonction Dial() d'Asterisk, qui est utilisée pour composer un numéro ou appeler un autre appareil. Les paramètres de cette fonction sont les suivants :

SIP/201: C'est la destination vers laquelle l'appel est dirigé. Dans ce cas, il indique qu'Asterisk doit composer le canal SIP associé à l'extension 201.
5: C'est la durée maximale de la tentative d'appel, en secondes. Dans ce cas, si l'appel n'est pas répondu après 5 secondes, Asterisk arrêtera la tentative d'appel.

Dans notre cas pour l'exo final nous avons fait quelques changements : 

Le contexte pour lequel vous aller développer cette fonctionnalité s’appellera « [technicien] » 
Le numéro de téléphone x600 doit permettre de faire sonner à tour de rôle chaque téléphone du 
service de la façon suivante : 
 Téléphone 1 (101) sonne pendant 20s 
 Téléphone 2 commence à sonner 10s après le début de téléphone 1 et pendant 20s. 
 Téléphone 3 commence à sonner 10 seconde après début téléphone 2 et pendant 20s 
 Le premier téléphone qui décroche est celui qui récupère l'appel. 
 Le contexte « technicien » doit être accessible pour tous les utilisateurs de l’agence.

sip.conf :

```
[general] 
context = techniciens ; commentaires
bindport=5060 
bindaddr=0.0.0.0 
srvlookup=yes 
disallow=all 
allow=alaw 
allow=gsm 
directmedia=no 
language=fr 
type=friend 
[101] 
host=dynamic 
username=101 
type=friend 
secret=789

[102] 
host=dynamic 
username=102
type=friend 
secret=789
[201] 
host=dynamic 
username=201 
type=friend 
secret=789

[202] 
host=dynamic 
username=202
type=friend 
secret=789

```

Et extentions.conf : 
```
[general]
[globals]
[technicien] 
exten => 101,1,Dial(SIP/101,10)
exten => 102,1,Dial(SIP/102) 
exten => 201,1,Dial(SIP/201,10)
exten => 202,1,Dial(SIP/202) 

```
Voici le modification du fichier extentions.conf
```
[general]
[globals]
[technicien]
exten => 101,1,Dial(SIP/101,10)
exten => 102,1,Dial(SIP/102) 
exten => 201,1,Dial(SIP/201,10)
exten => 202,1,Dial(SIP/202) 
exten => 1600,1,Verbose(2,Dialing techniciens sequentially)
 same => n,Dial(Local/technicien_1@TimeDelay&Local/technicien_2@TimeDelay&Local/technicien_3@TimeDelay,40)
 same => n,Hangup()

[LocalSets]
[TimeDelay]
exten => technicien_1,1,Verbose(2,Dialing technicien 1)
 same => n,Dial(SIP/101,20)
 same => n,Hangup()
exten => technicien_2,1,Verbose(2,Dialing technicien 2 with delay)
 same => n,Wait(10)
 same => n,Dial(SIP/102,20)
 same => n,Hangup()
exten => technicien_3,1,Verbose(2,Dialing technicien 3 with delay)
 same => n,Wait(20)
 same => n,Dial(SIP/201,20)
 same => n,Hangup()

```

[general], [globals], [technicien], [LocalSets], [TimeDelay]: Ce sont des sections de configuration pour différents aspects du système.

exten => 101,1,Dial(SIP/101,10): Lorsque l'extension 101 est composée, elle fait un appel vers l'extension SIP 101 avec un délai de 10 secondes.

exten => 102,1,Dial(SIP/102): Lorsque l'extension 102 est composée, elle fait un appel vers l'extension SIP 102.

exten => 201,1,Dial(SIP/201,10): Lorsque l'extension 201 est composée, elle fait un appel vers l'extension SIP 201 avec un délai de 10 secondes.

exten => 202,1,Dial(SIP/202): Lorsque l'extension 202 est composée, elle fait un appel vers l'extension SIP 202.

exten => 1600,1,Verbose(2,Dialing techniciens sequentially): Lorsque l'extension 1600 est composée, elle affiche un message verbeux indiquant que les techniciens sont appelés séquentiellement.

same => n,Dial(Local/technicien_1@TimeDelay&Local/technicien_2@TimeDelay&Local/technicien_3@TimeDelay,40): Il compose les extensions technicien_1, technicien_2 et technicien_3 en utilisant une séquence, en leur appliquant un délai spécifique, puis il les appelle toutes en même temps. Si l'appel n'est pas répondus dans les 40 secondes, il continue au prochain pas.

same => n,Hangup(): Il raccroche l'appel à la fin de la séquence.



Dans la section [TimeDelay], les extensions technicien_1, technicien_2 et technicien_3 sont configurées pour composer séquentiellement les techniciens, chacun avec un délai spécifique avant l'appel.



```
Directeur=SIP/101
Secretaire=SIP/102
DeptRT=SIP/201
DeptInfo=SIP/202

[interne]
exten => _XXX,1,Set(temp=${EXTEN})
	same => n,GotoIfTime(9:00-14:00,mon-fri,*,*?time,s,1:)
	same=>n,Hangup()
	
[time]
exten => s,1,Dial(SIP/${temp},5)
```
Voici l'explication : 

Directeur=SIP/101 : Cela assigne l'extension "Directeur" au numéro SIP 101.

Secretaire=SIP/102 : Cela assigne l'extension "Secretaire" au numéro SIP 102.

DeptRT=SIP/201 : Cela assigne l'extension "DeptRT" au numéro SIP 201.

DeptInfo=SIP/202 : Cela assigne l'extension "DeptInfo" au numéro SIP 202.

[interne] : C'est une autre section définissant les extensions pour le groupe "interne".

exten => _XXX,1,Set(temp=${EXTEN}) : Cette ligne définit une extension pour les numéros composés de trois chiffres (XXX). Elle stocke le numéro composé dans la variable temporaire "temp".

same => n,GotoIfTime(9:00-14:00,mon-fri,*,*?time,s,1:) : Cette ligne vérifie si l'appel est fait entre 9h et 14h du lundi au vendredi. Si c'est le cas, elle passe à l'étiquette "time" dans la priorité 1. Sinon, elle passe à la prochaine priorité.

same => n,Hangup() : Cette ligne raccroche l'appel si l'heure ou le jour n'est pas dans la plage spécifiée.

[time] : C'est une section qui définit les extensions pour le traitement des appels pendant certaines plages horaires.

exten => s,1,Dial(SIP/${temp},5) : Cette ligne compose l'extension "s" et appelle le numéro SIP stocké dans la variable temporaire "temp" pendant une durée de 5 secondes.

Comment faire en sorte que ce soit les fichiers sons Français qui soient joués par défaut en 
modifiant le fichier sip.conf ? 
SIP.CONF 
…….. 
[general] 
….. 
Language=fr 

## Pour lire des fichiers audio voici un exemple
[interne]
exten => _XXX,1,Set(temp=${EXTEN})
	same => n,GotoIfTime(9:00-16:00,mon-fri,*,*?time,s,1:)
	same=>n,Hangup()
	
[time]
exten => s,1,Set(CHANNEL(language)=fr)
exten => s,1,Playback(/var/lib/asterisk/sounds/fr/demo-congrats)  ou exten => s,1,Playback(demo-congrats)

Asterisk est-il capable de traduire les fichiers ?? Non cependant si le ficher n'existe pas dans FR il ira chercher dans le fichier par défaut défini dans sip.conf(Language=fr)
les sons sont stockés dans /var/lib/asterisks/sounds/....


Pour demander un mot de passe pour autoriser l'appel :

exten => 555,1,Authenticate(32657) 
 	same => n,Goto (enregistrement,s,1) 

Pour faire enregistrer un message vocal puis l'écouter après avoir appuyé sur # :

[time] 
exten => s,1,Set(CHANNEL(language)=fr) 
	same => n,Playback(recorded) 
	same => n,Record(custom/fichier-%d.alaw) 
	same => n,Playback(beep) 
	same => n,Verbose(${RECORDED_FILE})
	same => n,Playback(${RECORDED_FILE}) 


Pour tomber directement sur une musique d'attente :

exten => 888,1,Answer() 
	same => 888,2,MusicOnHold(default)	


Mise en place d'un serveur vocal intéractif :


[interne]
Cette ligne définit un contexte appelé "interne". Les contextes sont des sections de configuration dans Asterisk qui regroupent des règles pour le traitement des appels.

exten => 555,1,Goto(SVI,s,1)
Cette ligne indique à Asterisk quoi faire lorsqu'un appel est reçu sur le numéro 555. Elle dit à Asterisk de sauter à la première priorité (1) du contexte "SVI" (Service à Valeur Ajoutée) et de l'extension "s" (qui est souvent utilisée comme point d'entrée par défaut dans un contexte) lorsque le numéro 555 est composé.

[SVI]
Cette ligne définit un autre contexte appelé "SVI".

exten => s,1,BackGround(recorded) 
same => n,waitexten(5)
Ces lignes spécifient ce qui se passe lorsque l'appel est dirigé vers le contexte "SVI" avec l'extension "s". La première priorité (1) joue un fichier audio préenregistré appelé "recorded" à l'appelant. Ensuite, la fonction waitexten(5) permet à l'appelant de saisir une touche pendant 5 secondes.

exten => 1,1,Dial(SIP/102)
Cette ligne spécifie ce qui se passe lorsque l'appelant appuie sur la touche "1" pendant la lecture du fichier audio ou dans les 5 secondes suivantes. Dans ce cas, l'appel est dirigé vers l'extension SIP "102".

exten => 2,1,Dial(SIP/201)
Cette ligne spécifie ce qui se passe lorsque l'appelant appuie sur la touche "2" pendant la lecture du fichier audio ou dans les 5 secondes suivantes. Dans ce cas, l'appel est dirigé vers l'extension SIP "201".

Soit le code suivant : 

```
[interne]

exten => 555,1,Goto(SVI,s,1)

	
[SVI]
exten => s,1,BackGround(recorded) 
	same => n,waitexten(5)
	
exten => 1,1,Dial(SIP/102)

exten => 2,1,Dial(SIP/201)

```
