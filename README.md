# 🎵 Fiche Client - Compositeur Musique à l'Image

Application web interactive pour les compositeurs de musique à l'image afin de recueillir toutes les informations essentielles d'un projet client.

## ✨ Fonctionnalités Principales

### 📋 Questionnaire Complet
- **8 sections thématiques** couvrant tous les aspects d'un projet musical
- **Système de morceaux dynamiques** : ajoutez autant de morceaux que nécessaire
- **8 champs prioritaires** marqués comme "ESSENTIEL" pour ne rien oublier
- **Sauvegarde automatique** dans le navigateur (localStorage)

### 🎯 Mode Essentiel
Basculez entre le mode complet et le mode essentiel pour :
- Afficher uniquement les **champs critiques** lors des rendez-vous rapides
- Masquer temporairement les sections secondaires
- Progression adaptée au mode actif

### 📊 Exports Multiples
- **Export Excel** : Fichier `.xlsx` multi-onglets professionnel avec :
  - Dashboard récapitulatif
  - 9 onglets thématiques organisés
  - Indicateurs de progression
- **Export TXT** : Format texte simple et lisible
- **Export/Import JSON** : Sauvegarde complète pour backup

### 🎨 Interface Optimisée
- Design moderne et responsive
- Champs de saisie adaptés aux rendez-vous clients
- Indicateur de progression en temps réel
- Quick notes sur les informations cruciales
- Focus visuel amélioré

## 🚀 Utilisation

### Démarrage Rapide
1. Ouvrir le fichier `composer-client-checklist (1).html` dans votre navigateur
2. Remplir les informations du projet
3. Les données sont **sauvegardées automatiquement**

### Raccourcis Clavier
- `Ctrl + S` : Sauvegarder manuellement
- `Ctrl + E` : Exporter en TXT

### Mode Essentiel
Cliquez sur le bouton **"🎯 Mode Essentiel"** en haut à gauche pour afficher uniquement les champs prioritaires.

## 📑 Sections du Questionnaire

1. **📋 Informations générales** - Type de projet, durée, synopsis
2. **💰 Aspects financiers** - Budget, rémunération, paiement
3. **🎼 Besoins musicaux** - Morceaux détaillés avec système dynamique
4. **📅 Planning** - Deadlines, étapes, flexibilité
5. **🎧 Aspects techniques** - Formats, mixage, synchronisation
6. **⚖️ Droits juridiques** - SACEM, cession de droits, contrat
7. **🤝 Collaboration** - Validation, révisions, communication
8. **➕ Compléments** - Temp track, contraintes, facturation

## 📦 Sauvegarde et Export

### Sauvegarde Automatique
Les données sont sauvegardées automatiquement dans le navigateur toutes les 500ms après modification.

### Export Excel
Génère un fichier `.xlsx` professionnel avec :
- **Dashboard** : Vue d'ensemble avec indicateurs clés
- **9 onglets thématiques** : Une organisation claire par sujet
- **Prêt à partager** : Format professionnel pour vos clients

### Import/Export JSON
Pour sauvegarder ou transférer vos données :
1. Exporter en JSON (bouton "📥 Importer" puis fonction console)
2. Importer un fichier JSON existant

## 🔒 Confidentialité

Toutes les données sont stockées **localement dans votre navigateur**. Aucune information n'est envoyée sur Internet.

⚠️ **Navigation privée** : La sauvegarde automatique ne fonctionne pas en mode navigation privée. Pensez à exporter régulièrement vos données.

## 🆕 Nouvelles Fonctionnalités (Version Actuelle)

### Ajouts Récents
- ✅ Export Excel multi-onglets avec dashboard
- ✅ Mode Essentiel/Complet avec toggle
- ✅ Badges de priorité sur champs critiques
- ✅ Debouncing de sauvegarde (performances)
- ✅ Gestion d'erreur localStorage améliorée
- ✅ UX optimisée pour rendez-vous clients
- ✅ Quick notes sur informations cruciales

### Rétrocompatibilité
✅ Les anciens fichiers JSON restent 100% compatibles et importables.

## 💡 Bonnes Pratiques

### Pendant un Rendez-vous Client
1. Activer le **Mode Essentiel** pour se concentrer sur les priorités
2. Remplir les 8 champs "ESSENTIEL" en premier
3. Ajouter les morceaux au fur et à mesure de la discussion
4. Revenir au Mode Complet pour compléter les détails

### Gestion des Données
1. **Exporter régulièrement** en Excel pour archivage
2. **Sauvegarder en JSON** avant de vider le cache du navigateur
3. **Tester l'import** après export pour vérifier l'intégrité

## 🛠️ Technique

### Stack Technique
- **HTML5** pur (pas de build)
- **CSS3** avec variables CSS
- **JavaScript vanilla** (pas de framework)
- **Bibliothèque XLSX.js** pour l'export Excel (CDN)

### Compatibilité
- ✅ Tous les navigateurs modernes
- ✅ Desktop et tablette (responsive)
- ✅ Aucune installation requise
- ✅ Fonctionne en local (offline)

## 📄 Licence

Ce projet est destiné à un usage professionnel pour les compositeurs de musique à l'image.

---

**Version actuelle** : Avec export Excel, Mode Essentiel, et badges de priorité
**Dernière mise à jour** : Novembre 2025
