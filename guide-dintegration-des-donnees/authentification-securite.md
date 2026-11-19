---
description: Modes d'authentification des services web et bonnes pratiques de sécurité.
---

# Authentification et sécurité

## Services web d'échange (SOAP et REST)

Les services web authentifient l'appelant dans l'application. Trois modes sont acceptés :

| Mode                              | Principe                                                                                                                                                       | Transmission                                                                                                                                  |
| --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Informations d'appel (CommonInfo) | Clé de protection de l'API, identifiant et mot de passe de l'utilisateur. En cas de succès, Nomadia Field Service crée une session et renvoie son identifiant. | Bloc CommonInfo du corps de la requête, ou en-tête HTTP commonInfo (JSON encodé en base64). La clé peut aussi être passée dans l'en-tête KEY. |
| Session                           | Réutilisation de l'identifiant de session renvoyé par un premier appel.                                                                                        | Champ SessionId de la requête ou en-tête HTTP sessionId.                                                                                      |
| Jeton porteur (bearer)            | Jeton OAuth2 / OpenID Connect émis par un fournisseur d'identité externe, ou jeton émis par Nomadia Field Service lui-même.                                    | En-tête Authorization: Bearer \<jeton>.                                                                                                       |

### Bloc CommonInfo

| Élément      | Obligatoire  | Description                                                                                                                                    |
| ------------ | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Version      | Oui          | Version du format ; valeur fixe 1.                                                                                                             |
| Key          | Oui          | Clé de protection de l'API, fournie par Nomadia pour l'instance. La vérification est désactivée si aucune clé n'est configurée sur le serveur. |
| Language     | Non          | Langue des messages ; défaut en.                                                                                                               |
| UserLogin    | Oui          | Identifiant de l'utilisateur Nomadia Field Service au nom duquel l'appel est réalisé.                                                          |
| UserPassword | Non (schéma) | Mot de passe de l'utilisateur. Le serveur peut l'exiger (paramètre webservice.isUserPasswordRequired, activé par défaut).                      |

La durée d'inactivité d'une session est réglée côté serveur (sessionTimeOutInSecond, 3 600 secondes par défaut). Une session expirée renvoie l'erreur SESSION\_NOT\_FOUND (code 10) ; il faut alors s'authentifier de nouveau.

## Bonnes pratiques de sécurité

* Créez un compte utilisateur dédié à chaque intégration ; ne partagez pas un compte nominatif.
* Transmettez les secrets (clé, mot de passe, jeton) uniquement en HTTPS et stockez-les dans un coffre-fort côté client. Pour la circulation, utilisez le coffre-fort Nomadia Field Service (références ${vault:…}) décrit dans [Sécuriser les identifiants avec le coffre-fort](../module-circulation/coffre-fort.md).
* Réutilisez la session ou le jeton plutôt que de transmettre l'identifiant et le mot de passe à chaque appel.
* Renseignez l'en-tête HTTP EXTERN\_APP avec le nom de votre application : il est repris dans le journal des connexions API et facilite le diagnostic.
