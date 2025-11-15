# 🚀 Guide de Setup - SkyWar

## ÉTAPE 1 — Installer Haxe et les libs nécessaires

### Installation de Haxe
1. Télécharger Haxe depuis : https://haxe.org/download/
2. Installer Haxe sur votre système

### Dépendances identifiées

#### Pour le CLIENT (Flash/SWF) :
- **mt.bumdum** : Librairie MotionTwin (animation/effets)
  - `haxelib install mt-bumdum` (si disponible)
  - Ou utiliser les sources si présentes dans le projet

#### Pour le SERVEUR :
Le code serveur utilise des classes `db.*` (base de données) qui ne sont pas présentes dans ce dépôt :
- `db.Game`
- `db.Isle`
- `db.Unit`
- `db.GameUser`
- `db.Travel`
- `db.Log`
- `db.Fight`
- `App.gamedb`

**⚠️ IMPORTANT** : Le code serveur complet n'est pas présent dans ce dépôt. Il manque :
- La couche de base de données (`db.*`)
- La classe `App` principale
- Le point d'entrée du serveur (`Main.hx` ou équivalent)

### Commandes Haxe à exécuter

```bash
# Installer Haxe (si pas déjà fait)
# Windows: télécharger l'installateur depuis haxe.org
# Linux/Mac: utiliser le gestionnaire de paquets

# Vérifier l'installation
haxe --version

# Installer les librairies (si nécessaires)
# Note: certaines librairies peuvent être intégrées dans le projet
```

## ÉTAPE 2 — Recompiler le serveur Haxe

### Fichier de build serveur

Un fichier `web/build-server.hxml` a été créé pour compiler le serveur.

**⚠️ PROBLÈME** : Le code serveur complet n'est pas présent. Il faudra :
1. Localiser le code manquant (`db.*`, `App`, `Main.hx`)
2. Ou recréer la couche de base de données

### Compilation (une fois le code complet disponible)

```bash
cd web
haxe build-server.hxml
```

## ÉTAPE 3 — Lancer le serveur en local

Selon la cible de compilation (PHP, Neko, etc.) :

### Si compilé en PHP :
```bash
cd web/www
php -S localhost:8080
```

### Si compilé en Neko :
```bash
neko server.n
```

Le serveur doit répondre à :
- `http://localhost:8080/game/1/command.xml`

## ÉTAPE 4 — Faire tourner le client Flash

### Option A — Utiliser Ruffle (recommandé pour tester rapidement)

1. Télécharger Ruffle : https://ruffle.rs/
2. Installer l'extension navigateur ou utiliser la version desktop
3. Ouvrir les fichiers SWF :
   - `client/jeu/swf/base.swf`
   - `client/jeu/swf/gfx.swf`

### Option B — Recompiler le client en HTML5

Utiliser Haxe + OpenFL pour compiler vers HTML5 :
```bash
cd client/jeu
haxe client.hxml -js www/index.js
```

## ÉTAPE 5 — Connecter client ↔ serveur

Modifier `client/jeu/src/Api.hx` ligne 56 :

```haxe
// Avant :
var request = new haxe.Http("/game/"+Game.gameId+"/command.xml");

// Après (pour développement local) :
var request = new haxe.Http("http://localhost:8080/game/"+Game.gameId+"/command.xml");
```

Puis recompiler le client.

## ÉTAPE 6 — Jouer 🎉

Une fois tout configuré :
- Serveur local SkyWar opérationnel
- Client Flash ou HTML5 fonctionnel
- Possibilité d'héberger en ligne (OVH, AWS, etc.)

---

## ⚠️ PROBLÈMES IDENTIFIÉS

1. **Code serveur incomplet** : Les classes `db.*` et `App` sont manquantes
2. **Point d'entrée manquant** : Pas de `Main.hx` dans `web/src/`
3. **Dépendances externes** : `mt.bumdum` (MotionTwin) peut nécessiter une installation spéciale

## 📝 NOTES

- Le projet utilise Haxe pour compiler vers Flash (SWF) et serveur (PHP/Neko)
- Les fichiers SWF sont déjà compilés dans `client/*/swf/`
- Le dossier `web/www/` contient les assets graphiques
- Le code source est dans `client/*/src/` et `web/src/`

