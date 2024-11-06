---
icon: screwdriver
---

# A01 - Contrôles d'accès défaillants

🛠️ **A01 - Contrôles d'accès défaillants**

Dans cette vulnérabilité, la page est exposée à une faille **Insecure Direct Object Reference (IDOR)**, car l’ID utilisateur est directement accessible via l’URL sans vérification d’autorisation. L'ID d’utilisateur est en fait un hash MD5 du nom d'utilisateur, ce qui permet à un attaquant de manipuler l'URL pour accéder à d'autres comptes.

#### Détails de la vulnérabilité

En analysant le code source, on trouve le commentaire suivant :

```html
<!-- Si c'est l'administrateur admin_78 alors affiche le panneau de commande -->
```

Cela signifie que la page vérifiera l'ID dans l'URL pour déterminer si elle doit afficher le panneau de commande. En modifiant l'ID utilisateur dans l'URL, il est donc possible d'accéder au profil de l’administrateur sans permissions appropriées.

#### Exemple d'exploitation

Pour accéder au profil administrateur, nous devons obtenir le hash MD5 de l'identifiant `admin_78`. Le hash MD5 de `admin_78` est :

```
20541eeb668da7d30c80c56f00726f07
```

Avec cette information, nous pouvons accéder directement au profil de l'administrateur en utilisant l'URL suivante :

```
http://localhost:8042/profile.php?id=20541eeb668da7d30c80c56f00726f07
```

En accédant à cette URL, nous obtenons le flag de validation.

#### Solution et recommandations

Pour corriger cette vulnérabilité, il est essentiel de mettre en place une vérification d'autorisation adéquate sur le serveur. Voici quelques bonnes pratiques pour renforcer les contrôles d'accès :

1. **Vérifications côté serveur** : Assurez-vous que chaque requête est authentifiée et que l’utilisateur a les droits nécessaires pour accéder à l’objet.
2. **Éviter les identifiants exposés** : Utilisez des identifiants aléatoires et des mécanismes d’autorisation robustes plutôt que des identifiants simples comme des hashes d’informations sensibles.
3. **Contrôles d'accès basés sur les rôles** : Implémentez un système de rôles pour restreindre l'accès aux informations sensibles uniquement aux utilisateurs autorisés.
