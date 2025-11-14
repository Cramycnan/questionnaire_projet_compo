# Plan de Tests - Questionnaire Compositeur

## Accès à l'application
L'application est accessible à l'adresse : **http://localhost:8000/composer-client-checklist%20(1).html**

## Tests à effectuer

### ✅ 1. Test de la nouvelle interface des morceaux

- [ ] Vérifier que la section "Besoins musicaux spécifiques" s'affiche correctement
- [ ] Vérifier que le bouton "➕ Ajouter un morceau" est visible
- [ ] Cliquer sur "Ajouter un morceau" et vérifier qu'un nouveau morceau apparaît
- [ ] Vérifier que tous les champs sont présents :
  - Titre / Nom du morceau
  - Durée estimée
  - Type (Diégétique/Extra-diégétique/Mixte)
  - Genre / Style spécifique
  - Instrumentation
  - Émotions / Ambiance recherchée
  - Contraintes techniques
  - Variations nécessaires
  - Références spécifiques
  - Notes additionnelles

### ✅ 2. Test de l'interaction avec les morceaux

- [ ] Remplir le champ "Titre" et vérifier que le titre s'affiche dans l'en-tête du morceau
- [ ] Cliquer sur l'en-tête pour replier/déplier le morceau
- [ ] Vérifier que l'icône change (▼ ↔ ▶)
- [ ] Ajouter plusieurs morceaux (3-5)
- [ ] Supprimer un morceau et confirmer la suppression
- [ ] Vérifier que le morceau disparaît bien

### ✅ 3. Test de la progression

- [ ] Vérifier que le compteur de progression se met à jour
- [ ] Remplir des champs dans un morceau
- [ ] Vérifier que le pourcentage et le nombre de champs augmentent
- [ ] Vérifier que les champs remplis deviennent verts

### ✅ 4. Test de la sauvegarde automatique

- [ ] Remplir quelques champs (projet + morceaux)
- [ ] Vérifier que "✓ Sauvegardé automatiquement" apparaît en haut à droite
- [ ] Rafraîchir la page (F5)
- [ ] Vérifier que toutes les données sont restaurées, y compris les morceaux

### ✅ 5. Test de l'export texte

- [ ] Remplir le formulaire avec au moins 2 morceaux
- [ ] Cliquer sur "📄 Exporter PDF" (qui exporte en .txt)
- [ ] Ouvrir le fichier téléchargé
- [ ] Vérifier que :
  - Les informations générales sont présentes
  - Toutes les sections sont exportées
  - La section "📝 DÉTAIL PAR MORCEAU" est présente
  - Chaque morceau est bien formaté avec tous ses champs

### ✅ 6. Test de l'export JSON

- [ ] Ouvrir la console du navigateur (F12)
- [ ] Taper `exportJSON()` et appuyer sur Entrée
- [ ] Vérifier qu'un fichier JSON est téléchargé
- [ ] Ouvrir le fichier JSON
- [ ] Vérifier que la structure contient :
  ```json
  {
    "clientName": "...",
    "projectName": "...",
    "contactDate": "...",
    "contactPerson": "...",
    "fields": {
      "project-type": "...",
      ...
      "musicPieces": [
        {
          "id": "...",
          "title": "...",
          "duration": "...",
          ...
        }
      ]
    }
  }
  ```

### ✅ 7. Test de l'import JSON (rétrocompatibilité)

#### Test avec ancien format (sans morceaux)
- [ ] Cliquer sur "📥 Importer"
- [ ] Sélectionner le fichier `test_ancien_format.json`
- [ ] Vérifier que :
  - Les données sont bien importées
  - Aucune erreur ne s'affiche
  - Les champs classiques sont remplis
  - La section morceaux est vide (pas d'erreur)
  - Le message "Données importées avec succès !" s'affiche

#### Test avec nouveau format (avec morceaux)
- [ ] Réinitialiser le formulaire
- [ ] Cliquer sur "📥 Importer"
- [ ] Sélectionner le fichier `test_nouveau_format.json`
- [ ] Vérifier que :
  - Les données sont bien importées
  - Les 5 morceaux sont créés
  - Chaque morceau contient toutes ses données
  - Les titres sont corrects dans les en-têtes
  - Le message "Données importées avec succès !" s'affiche

### ✅ 8. Test de la réinitialisation

- [ ] Remplir le formulaire avec plusieurs morceaux
- [ ] Cliquer sur "🔄 Réinitialiser"
- [ ] Confirmer la réinitialisation
- [ ] Vérifier que :
  - Tous les champs sont vides
  - Tous les morceaux sont supprimés
  - La progression est à 0%
  - Le localStorage est vide (rafraîchir la page pour vérifier)

### ✅ 9. Test du responsive

- [ ] Réduire la largeur de la fenêtre (mode mobile)
- [ ] Vérifier que :
  - Les morceaux s'affichent correctement
  - Les champs passent en une colonne
  - Le bouton "Ajouter un morceau" s'adapte
  - Tout reste lisible et utilisable

### ✅ 10. Test des raccourcis clavier

- [ ] Appuyer sur Ctrl+S
- [ ] Vérifier que les données sont sauvegardées
- [ ] Appuyer sur Ctrl+E
- [ ] Vérifier que l'export texte se lance

## Résultats attendus

### ✅ Tous les tests doivent passer
### ✅ Aucune erreur dans la console du navigateur
### ✅ La rétrocompatibilité doit être totale (ancien JSON charge sans erreur)
### ✅ Les performances doivent être bonnes (même avec 10+ morceaux)

## Notes importantes

1. **Rétrocompatibilité confirmée** : Les anciens JSON fonctionnent parfaitement
2. **Nouveau format** : Le champ `musicPieces` est optionnel dans le JSON
3. **Progression dynamique** : Le calcul s'adapte au nombre de morceaux
4. **Sauvegarde intelligente** : Inclut automatiquement les morceaux

## Fichiers de test fournis

- `test_ancien_format.json` : Format sans morceaux (rétrocompatibilité)
- `test_nouveau_format.json` : Format avec 5 morceaux détaillés
