# 📋 Analyse du Projet SkyWar

## Structure des fichiers présents

### ✅ Fichiers SWF (Flash) - 4 fichiers trouvés
- `client/lecteur avatar/swf/gfx.swf`
- `client/jeu/swf/gfx.swf`
- `client/jeu/swf/base.swf`
- `client/bouilleur/swf/gfx.swf`

### ❌ Fichiers HTML, CSS, JS
- **Aucun fichier HTML trouvé**
- **Aucun fichier CSS trouvé**
- **Aucun fichier JS trouvé**

### 📁 Structure des dossiers

#### Client (Flash)
- `client/jeu/` : Jeu principal
  - `src/` : Code source Haxe (Api.hx, Game.hx, Manager.hx, etc.)
  - `swf/` : Fichiers SWF compilés
  - `fla/` : Fichiers Flash source (.fla)
  - `bmp/` : Images bitmap
- `client/bouilleur/` : Outil de création
- `client/lecteur avatar/` : Lecteur d'avatar
- `client/avatar/` : Assets d'avatar

#### Serveur/Backend
- `web/src/` : Code serveur Haxe
  - `fight/` : Logique de combat (Resolver.hx, Logger.hx, etc.)
  - `flash/` : Code serveur pour Flash (Player.hx, Progression.hx, etc.)
  - Classes métier : Building.hx, Yard.hx, BotMap.hx, etc.
- `web/www/` : Assets web (images, graphiques)
  - `gfx/` : 848+ fichiers graphiques (PNG, JPG, GIF)

#### Code partagé
- `com/` : Code commun client/serveur
  - Protocol.hx : Protocole de communication
  - Datas.hx : Structures de données
  - GamePlay.hx : Logique de jeu
  - BuildingLogic.hx, ShipLogic.hx : Logiques métier

### 🔍 Code serveur - Classes utilisées mais manquantes

Le code dans `web/src/` fait référence à des classes qui ne sont **pas présentes** dans le dépôt :

#### Classes `db.*` (Base de données)
- `db.Game` : Gestion des parties
- `db.Isle` : Gestion des îles
- `db.Unit` : Gestion des unités/vaisseaux
- `db.GameUser` : Gestion des joueurs
- `db.Travel` : Gestion des voyages
- `db.Log` : Système de logs
- `db.Fight` : Gestion des combats

#### Classe `App`
- `App.gamedb` : Accès à la base de données du jeu

#### Point d'entrée
- `Main.hx` : Point d'entrée du serveur (absent)

### 📡 Communication Client-Serveur

Le client Flash communique avec le serveur via :
- **Endpoint** : `/game/{gameId}/command.xml`
- **Méthode** : POST avec paramètres encodés
- **Format** : XML avec données sérialisées Haxe
- **Fichier** : `client/jeu/src/Api.hx` (ligne 56)

### 🔧 Fichiers de configuration

#### Fichiers .hxml (build Haxe)
- `client/jeu/client.hxml` : Build client Flash
- `client/bouilleur/client.hxml` : Build bouilleur
- `client/lecteur avatar/client.hxml` : Build lecteur avatar
- `web/build-server.hxml` : **Créé** pour build serveur (nécessite code complet)

#### Fichiers .xml (SWF)
- `client/jeu/swfmake.xml` : Configuration compilation SWF
- `client/bouilleur/swfmake.xml`
- `client/lecteur avatar/swfmake.xml`

### 📦 Dépendances identifiées

#### Client
- `mt.bumdum.Lib` : Librairie MotionTwin (animations)
- `mt.bumdum.Trick` : Librairie MotionTwin (effets)
- `mt.net.Codec` : Librairie MotionTwin (encodage réseau)

#### Serveur
- Classes `db.*` : ORM ou couche de base de données (manquante)
- Classe `App` : Application principale (manquante)

### ⚠️ Problèmes identifiés

1. **Code serveur incomplet** : Les classes de base de données sont absentes
2. **Point d'entrée manquant** : Pas de `Main.hx` dans `web/src/`
3. **Dépendances externes** : `mt.bumdum` (MotionTwin) peut nécessiter installation
4. **Pas de fichiers HTML** : Le jeu est 100% Flash, nécessite Ruffle ou recompilation HTML5

### ✅ Ce qui fonctionne

- Les fichiers SWF sont compilés et peuvent être ouverts avec Ruffle
- Le code source client est présent et compilable
- Les assets graphiques sont présents dans `web/www/gfx/`
- Le protocole de communication est défini dans `com/Protocol.hx`

### 🎯 Prochaines étapes

1. Localiser ou recréer les classes `db.*` et `App`
2. Créer le point d'entrée `Main.hx` pour le serveur
3. Installer les dépendances Haxe nécessaires
4. Compiler le serveur
5. Tester avec Ruffle ou recompiler en HTML5

