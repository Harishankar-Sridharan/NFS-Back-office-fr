---
description: >-
  Médiums d'entrée et de sortie de la circulation, paramètres des répertoires
  surveillés et nom des fichiers produits.
---

# Médiums

Un médium est un canal d'entrée ou de sortie : répertoire, SFTP/FTP, HTTP, JMS, boîte mail… Les médiums se déclarent dans la section `mediums` d'un bloc.

## Médiums d'entrée (input-mediums)

| Balise                         | Rôle                                                                                                             | Paramètres principaux                                                                                                                     |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `directory-input-medium`       | Surveille un répertoire : chaque fichier est un message.                                                         | voir ci-dessous                                                                                                                           |
| `url-input-medium`             | Même rôle sur un serveur FTP ou SFTP.                                                                            | mêmes paramètres (sélecteurs `addedFiles`, `allFiles`, `filesList`), `url-trigger`, `sftp-private-key-file-location`                      |
| `http-input-medium`            | Publie une URL de la circulation (voir [Recevoir des messages par HTTP](../exemples/recevoir-messages-http.md)). | `name`, `synch` (défaut `true`)                                                                                                           |
| `mailbox-input-medium`         | Interroge une boîte aux lettres : chaque mail ou pièce jointe est un message.                                    | `mail-session` ou `jndi-name`, `folder` (défaut `INBOX`), `cron-periodicity`, `handle-raw`, `handle-attachement`, `handle-inline`         |
| `jms-input-queue`              | Lit une file JMS.                                                                                                | `jndi-name`, `jms-connection`, `acknowledge-mode`                                                                                         |
| `storage-queue-input-medium` ◆ | Lit une file de stockage cloud et active un écouteur.                                                            | `cron-periodicity`, `activable-listener`, `begin-ticket-status`, `end-ticket-status`                                                      |
| `backup-medium`                | Sauvegarde les enregistrements exportés pour pouvoir les rejouer.                                                | `backup-strategy` (`BACKUP_ONLY`, `BACKUP_THEN_SEND`, `BACKUP_THEN_SEND_WITH_LASTFAILURES`), `max-try-before-skip`, `max-backup-elements` |

### Paramètres de directory-input-medium

| Balise                                  | Rôle                                                                                                                                                               |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `location`                              | Répertoire surveillé (créé s'il n'existe pas). Chemin relatif possible avec `root-path-connection`.                                                                |
| `message-selector`                      | Fichiers pris en compte à chaque scan (voir tableau suivant). Défaut : `allFiles`.                                                                                 |
| `trigger-files-list`                    | Mots-clés séparés par « \| » : tous doivent correspondre à un fichier présent pour lancer le traitement, dans l'ordre des mots-clés. Obligatoire avec `filesList`. |
| `scan-time-interval`                    | Intervalle entre deux scans, en millisecondes. Ne pas combiner avec un déclencheur.                                                                                |
| `directory-trigger` / `instant-trigger` | Déclencheur qui pilote les scans (voir [Déclencheurs et interrupteurs](declencheurs-interrupteurs.md)). Recommandé quand de nombreux répertoires sont surveillés.  |
| `delete-on-success`                     | Supprime le fichier après un traitement réussi. Défaut : `true`.                                                                                                   |
| `nb-max-try`                            | Nombre maximal de tentatives avant abandon. Sans valeur : tentatives illimitées.                                                                                   |
| `failure-trash-location`                | Répertoire où sont déplacés les fichiers abandonnés.                                                                                                               |
| `detected-backup-location`              | Répertoire où une copie datée de chaque fichier détecté est conservée.                                                                                             |
| `contextualSubLocationPattern`          | Sous-répertoire ajouté selon le contexte, avec des champs du modèle d'échange (ex. `[AREAID]`).                                                                    |
| `charset-name`                          | Encodage de lecture des fichiers.                                                                                                                                  |

### Valeurs de message-selector

| `message-selector`          | Fichiers traités                                                                                 |
| --------------------------- | ------------------------------------------------------------------------------------------------ |
| `allFiles` (défaut)         | Tous les fichiers présents à chaque scan.                                                        |
| `allFilesAlphabeticalOrder` | Tous les fichiers, triés par nom.                                                                |
| `addedFiles`                | Uniquement les fichiers ajoutés depuis le scan précédent.                                        |
| `filesList`                 | Lots de fichiers définis par `trigger-files-list`.                                               |
| `zipFile`                   | Une archive ZIP à la fois : elle est décompressée et chaque fichier qu'elle contient est traité. |

Exemple du mode `filesList` : mots-clés `gss_commandes|gss_clients|gss_absences_techniciens` et fichiers présents :

* `gss_commandes_05-06.csv` et `gss_commandes_06-06.csv` ;
* `gss_clients_05-06.csv` ;
* `gss_absences_techniciens_05-06.csv`.

Seul le lot du 05-06 est traité. Le fichier `gss_commandes_06-06.csv` attend l'arrivée de nouveaux fichiers clients et absences.

## Médiums de sortie (output-mediums)

| Balise                            | Rôle                                                                  | Paramètres principaux                                                                                                  |
| --------------------------------- | --------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `directory-output-medium`         | Écrit chaque message dans un fichier d'un répertoire.                 | `location`, `prefix`, `suffix` ou `filename-pattern`, `root-path-connection`, `contextualSubLocationPattern`           |
| `directory-output-medium-v2`      | Même rôle avec choix de l'encodage.                                   | idem + `charset-name`                                                                                                  |
| `url-output-medium`               | Même rôle vers un serveur FTP ou SFTP.                                | idem + `sftp-private-key-file-location`                                                                                |
| `file-output-medium`              | Ajoute les messages à la suite dans un fichier unique (journal).      | `location`, `roll-size` (Ko, archivage au-delà), `charset-name`                                                        |
| `mail-output-medium`              | Envoie un e-mail ; le corps est produit par le transformateur.        | `mail-session` ou `jndi-name`, `from`, `to`, `cc`, `bcc`, `subject`, `mime-type`                                       |
| `mail-attachment-output-medium`   | Envoie un e-mail avec le message en pièce jointe.                     | `from`, `to`/`cc`/`bcc`, `dest`, `msg`, `msg-subject`, `filename-pattern`, `skip-sending-empty-attachments`, `headers` |
| `mail2sms-output-medium`          | Envoie un SMS via la passerelle e-mail d'un fournisseur.              | comme un e-mail + `mail-domain-name`                                                                                   |
| `sms-output-medium`               | Envoie un SMS via l'interface HTTP d'un fournisseur.                  | `url`, `verb`, `resp-analyzer`, `query-params`                                                                         |
| `all-my-sms-output-medium` ◆      | Envoie un SMS via le service AllMySMS.                                | `clientcode`, `passcode`                                                                                               |
| `message-output-medium`           | Crée un message applicatif pour des ressources Nomadia Field Service. | `from`, `dest`, `msg`, `publicationStartDate`, `publicationEndDate`, `ExpectReply`, `Confidential`, `Emergency`        |
| `http-output-medium`              | Envoie le message en POST ; réussi si le serveur répond 200.          | `url`, `http-connection`, `http-init-connection` (obtention d'un jeton)                                                |
| `rest-output-medium`              | Appelle un service REST.                                              | `url`, `verb`, `content-type`, `http-connection`, `http-init-connection`, `resp-analyzer`, `query-params`              |
| `office-calendar-output-medium` ◆ | Met à jour un calendrier Office 365.                                  | `verb` (`KIND_CREATE`, `KIND_UPDATE`, `KIND_DELETE`), paramètres Azure AD                                              |
| `storage-queue-output-medium` ◆   | Envoie le résultat dans une file de stockage cloud.                   | `result-content-name`, `push-ticket-result`                                                                            |
| `jms-output-queue`                | Envoie dans une file JMS (messages persistants).                      | `jndi-name`, `jms-connection`                                                                                          |
| `log`                             | Écrit dans le journal général de l'application.                       | `prefix`                                                                                                               |

### Nom des fichiers produits

Sans `filename-pattern`, le nom est construit ainsi : `[prefix][date et heure de création][suffix]`. Avec `filename-pattern`, les repères suivants sont remplacés :

| Repère | Valeur                                  |
| ------ | --------------------------------------- |
| `{0}`  | Date et heure de création               |
| `{1}`  | Identifiant du message                  |
| `{2}`  | Nom du médium                           |
| `{3}`  | Nom du support (ex. fichier d'origine)  |
| `{4}`  | Indicateur de ligne (messages découpés) |
| `{5}`  | Nom du contexte de circulation          |
| `{6}`  | Nombre aléatoire                        |

Exemple : `result-{0}-{3}-{6}.csv`.

### Paramètres des requêtes REST et SMS (var-marshaller)

| Valeur                                        | Contenu du paramètre                                                                                                |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `CIRC_MESSAGE`                                | Message reçu par le médium.                                                                                         |
| `CIRC_PARAM`                                  | Champ du modèle d'échange (indiqué dans `var-value`) d'une entité du contexte.                                      |
| `RESOURCE_CIRC_PARAM`                         | Texte d'une ressource `notifier.properties` (nom dans `var-value`) complété par les champs de l'entité du contexte. |
| `RESOURCE_MESSAGE`                            | Texte d'une ressource `notifier.properties`.                                                                        |
| `LOGIN`, `PASSWORD`, `PHONE`, `UNKNOWN` (SMS) | Compte, mot de passe, numéro du destinataire, valeur fixe de `var-value`.                                           |
