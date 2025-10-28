# Suivi des heures – Chantier

Application web statique pour saisir, suivre et imprimer les heures par chantier, ouvrier et poste. Aucune base de données ni serveur requis: les données sont stockées dans le navigateur (localStorage) et peuvent être exportées/importées en JSON ou partagées via une URL.

## Fonctionnalités

- Saisie rapide des entrées (date, poste, ouvrier, heures normales/supplémentaires, commentaire).
- Filtres par jour ou semaine ISO.
- Récaps par ouvrier et par poste (semaine filtrée).
- Multi-chantiers: onglets, ajout, renommage, suppression (données isolées par chantier).
- Impression:
  - Imprimer semaine (vue filtrée)
  - Imprimer récap chantier (totaux par ouvrier et par poste)
- Export/Import:
  - Exporter JSON
  - Exporter CSV (toutes les entrées)
  - Importer JSON
  - Partager URL: génère un lien contenant les données pour import automatique

## Utilisation

- Ouvrir `index.html` dans un navigateur moderne (Chrome, Edge, Firefox, Safari récents).
- Renseigner les entrées dans la section “Saisie”.
- Utiliser le filtre “Filtrer par semaine” ou cliquer sur une date pour filtrer le jour.
- Gérer les chantiers depuis la barre d’en-tête (onglets + boutons “+ Chantier”, “Renommer”, “Supprimer”).

## Données et stockage

- Stockage local via `localStorage` du navigateur.
- Données isolées par chantier: chaque chantier possède ses propres clés de stockage suffixées par un slug.
- Aucune donnée côté serveur.

## Partage des données

- Bouton “Partager URL”:
  - Génère un lien avec les données du chantier courant encodées dans le fragment (`#share=...`).
  - Le lien est copié dans le presse-papiers.
  - Ouvrir ce lien dans un autre navigateur importe automatiquement le chantier, ses listes et entrées, puis nettoie le `#share`.
- Limites:
  - La taille de l’URL doit rester raisonnable (OK pour un historique standard).
  - Le lien contient les données en clair: à partager uniquement avec des personnes de confiance.

## Import / Export

- Export JSON: génère un fichier `oleron_heures.json`.
- Export CSV: génère un fichier `oleron_heures.csv`.
- Import JSON: charge un fichier au format `{ entries, postes, ouvriers }`. Les entrées sont normalisées (format hh:mm, semaine ISO, etc.).

## Impression

- Imprimer semaine: imprime la vue filtrée (avec un titre Semaine X – Année).
- Imprimer récap chantier: affiche une page de synthèse par ouvrier et par poste, puis lance l’impression.

## Déploiement (GitHub Pages)

1. Créer un dépôt GitHub et y ajouter `index.html` (et ce `README.md`).
2. GitHub → Settings → Pages → Build and deployment:
   - Source: Deploy from a branch
   - Branch: `main` (root)
3. Attendre l’URL fournie par GitHub Pages (ex: `https://<user>.github.io/<repo>/`).
4. Ouvrir l’URL. Les données restent locales (dans le navigateur de chaque appareil).

## Compatibilité navigateurs

- Chrome, Edge, Firefox, Safari récents.
- Le partage d’URL et l’import automatique fonctionnent sans dépendances.
- Le bouton “Partager URL” utilise l’API du presse-papiers si disponible, sinon propose une copie manuelle.

## Développement

- Projet monofichier: tout est dans `index.html` (HTML/CSS/JS).
- Aucune dépendance externe.
- Les clés de stockage:
  - Projets: `oleron_projects_v1`
  - Projet courant: `oleron_current_project_v1`
  - Données par chantier: `oleron_entries_v1__<slug>`, `oleron_postes_v1__<slug>`, `oleron_ouvriers_v1__<slug>`

## Sécurité et confidentialité

- Aucune donnée transmise à un serveur.
- Les données résident dans le navigateur tant qu’elles ne sont pas supprimées.
- Le lien de partage inclut les données en clair: traiter comme un document sensible.

## Licence

Libre d’usage interne. Adapter une licence si nécessaire.
