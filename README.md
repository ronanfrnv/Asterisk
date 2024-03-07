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
