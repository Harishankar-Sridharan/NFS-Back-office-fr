---
description: >-
  Stocker de façon chiffrée les identifiants et points d'accès utilisés par la
  circulation, et migrer une circulation existante vers le coffre-fort.
---

# Sécuriser les identifiants avec le coffre-fort

Le coffre-fort stocke, chiffrés, les identifiants et points d'accès utilisés par la circulation : mots de passe, comptes, clés, jetons, chaînes de connexion, URL de serveurs distants… Le fichier de circulation n'y fait plus que référence : il ne contient plus de secret en clair et peut être copié d'un environnement à l'autre sans exposer les accès de production.

## Avant de commencer

Le coffre-fort est configuré par l'exploitant du serveur, dans les paramètres du serveur, par une variable d'environnement ou par une propriété système.

| Paramètre serveur                                                                                                  | Rôle                                                                                                                                                                          | Valeur par défaut                           |
| ------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------- |
| `nfs.environment`                                                                                                  | Nom de l'environnement du serveur (ex. PROD, RECETTE). Le coffre refuse de s'ouvrir s'il a été créé pour un autre environnement.                                              | (vide)                                      |
| Clé maître : variable d'environnement `CREDENTIAL_VAULT_MASTER_KEY` (recommandée) ou `credential.vault.master-key` | Clé de chiffrement : 32 octets encodés en base64. Sans clé, le coffre est fermé.                                                                                              | aucune                                      |
| `credential.vault.backend`                                                                                         | Stockage : `database` (base de données de l'application, partagée par toutes les instances) ou `file` (fichier JSON du serveur).                                              | `database`                                  |
| `credential.vault.path`                                                                                            | Stockage fichier uniquement : emplacement du fichier du coffre.                                                                                                               | dans le répertoire de paramètres du serveur |
| `credential.vault.read-only`                                                                                       | Stockage fichier uniquement : `true` sur les instances qui lisent un coffre écrit par une autre instance.                                                                     | `false`                                     |
| `credential.vault.strict`                                                                                          | Mode strict : refuse les identifiants et points d'accès écrits en clair dans la circulation (voir la partie Migrer une circulation existante vers le coffre-fort ci-dessous). | `false`                                     |

{% hint style="danger" %}
Conservez une sauvegarde de la clé maître séparément du coffre : une clé perdue ne peut pas être récupérée. La clé ne doit jamais être placée dans le fichier de paramètres livré avec l'application : elle y est refusée.
{% endhint %}

## Accéder au coffre-fort

**Navigation :** `Administration > Fichiers XML > Coffre-fort`

L'écran affiche :

* l'**État du coffre** : **Stockage**, **Environnement**, **Fichier**, état **Ouvert** ou **Fermé** ;
* la liste des **Identifiants** : **Domaine**, **Identifiant**, **Propriétés**, **Mise à jour**.

## Référencer le coffre-fort dans la circulation

Dans le fichier de circulation, une valeur sensible est remplacée par une référence de la forme :

```
${vault:<identifiant>/<propriété>}
```

* Les identifiants utilisés par la circulation sont rangés dans le domaine `circulation` du coffre.
* Par convention, l'identifiant est l'`id` de l'objet qui utilise la valeur (connexion, médium…) ; la propriété est le nom de la balise (`password`, `user`, `location`…).
* Une référence peut constituer toute la valeur ou seulement une partie. Dans une URL, une référence placée dans la partie utilisateur / mot de passe est automatiquement encodée : les caractères `@`, `:` ou `/` du mot de passe ne cassent pas l'URL.
* Les références sont résolues au chargement de la circulation. Une référence introuvable empêche la circulation de démarrer.

Exemple : médium SFTP dont le compte et le mot de passe sont dans le coffre (identifiant `sftp-client`, propriétés `user` et `password`).

```xml
<output-mediums>
  <url-output-medium>
    <id>sftp-client</id>
    <location>sftp://${vault:sftp-client/user}:${vault:sftp-client/password}@sftp.client.fr:22/depot/nfs</location>
    <filename-pattern>interventions-{0}.csv</filename-pattern>
  </url-output-medium>
</output-mediums>
```

## Créer ou modifier un identifiant

1. Ouvrez `Administration > Fichiers XML > Coffre-fort`.
2. Cliquez sur **Nouvel identifiant**, ou ouvrez un identifiant existant.
3. Renseignez le **Domaine** (`circulation`) et l'**Identifiant** (sans barre oblique).
4. Pour chaque **Propriété**, saisissez son nom et sa **Nouvelle valeur**. Utilisez **Ajouter une propriété** pour en ajouter, cochez **Supprimer** pour en retirer.
5. Enregistrez.

**Résultat :** le message « Identifiant … enregistré : ajout …, remplacement …, suppression … » s'affiche. Les valeurs ne sont jamais réaffichées ; laisser une valeur vide conserve la valeur actuelle.

{% hint style="warning" %}
La circulation lit les valeurs du coffre à son démarrage : une modification du coffre n'est prise en compte qu'après le prochain redémarrage du serveur. La circulation n'est pas rechargée automatiquement.
{% endhint %}

## Migrer une circulation existante vers le coffre-fort

La fonction **Migration de la circulation** déplace automatiquement dans le coffre les identifiants et points d'accès écrits en clair dans le fichier de circulation du serveur, et les remplace par des références.

1. Ouvrez `Administration > Fichiers XML > Coffre-fort`, partie **Migration de la circulation**.
2. Cliquez sur **Analyser la circulation**. L'écran liste les valeurs à déplacer (**Élément de la circulation**, **Référence écrite à la place**) ou les points bloquants à corriger.
3. Corrigez les éventuels points bloquants dans le fichier (par exemple : élément sans `id` englobant, identifiant contenant une barre oblique, une accolade ou un espace).
4. Cliquez sur **Migrer la circulation** et confirmez.
5. Redémarrez le serveur, puis vérifiez le rapport de chargement de la circulation.
6. Une fois la circulation vérifiée, demandez l'activation du mode strict (`credential.vault.strict` = `true`).

**Résultat :** le message « … valeur(s) déplacée(s) dans le coffre. Copie de la circulation avant migration : … » s'affiche. Une copie horodatée du fichier d'origine est conservée.

## Points d'attention

* Les destinataires des e-mails (`to`, `cc`, `bcc`, `from`, `dest`) ne sont pas considérés comme sensibles : ils restent dans le fichier.
* Une URL distante est déplacée en entier (compte, mot de passe, serveur et chemin).
* Le mode strict refuse aussi : mots de passe, comptes, clés, jetons, chaînes de connexion, URL et noms de serveur, en-têtes ou paramètres HTTP contenant un identifiant, emplacements distants et partages réseau.
* Restaurer une base de production sur un serveur de test fait refuser l'ouverture du coffre (stockage `database`) : exportez le coffre de test avant la restauration (bouton **Exporter**) et réimportez-le après (bouton **Importer**).
* Si le coffre ne peut plus être ouvert et qu'aucun export n'existe, **Réinitialiser le coffre** supprime définitivement tous les identifiants ; le nom de l'environnement est demandé pour confirmer.
