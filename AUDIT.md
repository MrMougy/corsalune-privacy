# Vérification de confidentialité — 19 octobre 2026

## Périmètre

Lecture seule du projet Godot local, des scripts de jeu, du profil Android de publication, du manifeste fusionné release et du paquet `Corsalune-v0.1.1.aab`. Aucun fichier du jeu modifié. Le projet local comporte des changements non commités ; sa révision Git de base est `f58dd26c1a5df54270380a5d228b11e485e1f482`.

Paquet examiné : `org.corsalune.game`, version `0.1.1`, versionCode `2`.
SHA-256 AAB : `794fc95fc51f2af631eddcb9cc8215078ef992b51a8ff68b24f0fe12f7b21362`.

## Constats

- Profil release et manifeste : permission Internet absente, `allowBackup=false`, conservation après désinstallation désactivée. Aucune déclaration `uses-permission` dans le manifeste du bundle examiné. La permission DUMP protège un receiver AndroidX ; ce n'est pas une permission demandée par l'application.
- Un autre profil prototype utilise un autre identifiant et la vibration : il n'est pas le paquet couvert par cette politique. La version interne du projet Godot diffère également ; la politique suit la version Android de publication.
- Recherche des API réseau et d'URL dans les scripts : aucun appel réseau identifié. L'URL XML d'un SVG généré localement n'est pas une requête réseau.
- Sauvegardes : `scripts/state/save_game.gd`, stockage `user://saves`, JSON, copie `.bak`, fichier temporaire et conservation possible de fichiers illisibles.
- Réglages : `scripts/state/user_settings.gd`, stockage `user://settings`, préférences et copie de secours.
- Profil du capitaine : choix cosmétiques du personnage, sans identité réelle requise.
- Bibliothèques : moteur Godot et AndroidX dans la configuration Gradle et le manifeste. Pas d'extension publicitaire identifiée. Recherche de signatures dans les DEX du bundle négative pour Firebase, Crashlytics, Google Mobile Ads, Facebook, AppsFlyer, Adjust et Unity Ads. Cette recherche ciblée ne constitue pas un audit exhaustif du code natif.
- Aucun compte ou multijoueur dans le périmètre actuel ; confirmation également fournie par le développeur.
- Contact et nom public confirmés par l'utilisateur : MrMougy, corsalune.support@gmail.com.

## Limites et points de mise en production

Audit statique, sans interception réseau sur un appareil et sans accès à la Play Console. Vérifier que le bundle effectivement soumis correspond à celui examiné. Refaire l'audit si des SDK ou fonctionnalités réseau sont ajoutés.

Android peut autoriser des migrations appareil-à-appareil chez certains fabricants malgré `allowBackup=false`. La politique n'assimile donc pas cette option à une interdiction absolue de tout transfert.

La politique distingue le jeu, les échanges volontaires de support et la journalisation IP de GitHub Pages. Aucun script, cookie, formulaire, police distante ou outil d'analyse n'est ajouté au site.

Pour Play Console : renseigner l'URL de la politique et le formulaire Sécurité des données à partir du bundle distribué ; prévoir également un accès à la politique depuis le jeu, conformément aux règles Google Play. Cette tâche n'autorise aucune modification du jeu. Le nom public du développeur est confirmé ; vérifier les éventuelles obligations d'identification légale et les pratiques réelles de conservation de la boîte support.

## Références

- [Données utilisateur — Google Play](https://support.google.com/googleplay/android-developer/answer/10144311?hl=fr)
- [Sauvegardes Android et transferts](https://developer.android.com/identity/data/autobackup)
- [Journalisation des adresses IP par GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages)
