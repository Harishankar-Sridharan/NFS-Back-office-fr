---
description: Publier une URL de la circulation pour recevoir des messages par HTTP.
---

# Recevoir des messages par HTTP

Un médium `http-input-medium` publie une URL de la circulation de la forme :

```
https://<serveur>/<application>/circulation/<name>
```

où `<application>` est le chemin de l'application Nomadia Field Service (celui de la page de connexion) et `<name>` la valeur de la balise `name` du médium.

```xml
<http-input-medium>
  <id>http-import-interventions</id>
  <name>importInterventions</name>
</http-input-medium>
```

## Fonctionnement

* Le message est envoyé dans le corps d'une requête POST. Pour un test, il peut être passé en GET dans le paramètre `message`.
* Les autres paramètres de la requête sont transmis à la chaîne de traitement : ils peuvent par exemple alimenter une requête SQL (voir [Paramètres dynamiques des requêtes SQL](../reference/processeurs.md)).
* La réponse est toujours un document XML au format `circulation-result` (voir [Format de retour circulation-result](../reference/format-circulation-result.md)).
* Par défaut (`synch` absent ou `true`), les messages reçus sur une même URL sont traités l'un après l'autre ; des URL différentes sont traitées en parallèle. Avec `synch` à `false`, les messages d'une même URL peuvent être traités en parallèle : réservez ce mode aux traitements sans effet de bord (géocodage, consultation).

Pour lister et tester les URL publiées, consultez [Suivre et piloter la circulation](../suivre-piloter-circulation.md).

{% hint style="danger" %}
Par défaut, les URL de la circulation exigent une session Nomadia Field Service authentifiée. L'ouverture sans authentification est contrôlée par le paramètre serveur `circulation.http.listeners.openSecurity` (par défaut `false`) : ne l'activez que si l'accès réseau au serveur est maîtrisé.
{% endhint %}
