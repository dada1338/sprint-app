# SprintLab

Application web (un seul fichier `index.html`, aucune dépendance) pour mesurer, analyser et faire progresser la vitesse des sprinteurs. Ouvrez `index.html` dans un navigateur, sur ordinateur ou sur téléphone.

## Onglets

- **Équipe** : classement par vitesse max, 30 m projeté, tendance par athlète, fiche de progression, ajout d'athlètes, export/import JSON.
- **Chrono** : saisie des temps de passage (gabarits 20/30/60/100 m). Calcule la vitesse par segment et ajuste le modèle
  `v(t) = Vmax·(1 − e^(−t/τ))` : Vmax, τ, accélération initiale, distance à 95 % de Vmax.
- **Modèle** : course modèle 100 m pour un objectif de temps (réaction, τ, perte de vitesse en fin de course) :
  vitesse max requise, temps de passage tous les 10 m, courbes des temps voisins, comparaison avec une séance enregistrée.
- **Vidéo** : lecture image par image (ralenti, vidéos slow-motion 2×/4×/8×), mesure d'angles articulaires (3 points),
  inclinaison d'un segment par rapport à la verticale, marquage d'événements pour les temps de contact et de vol.

Les données sont stockées dans le navigateur (`localStorage`) ; les vidéos ne quittent jamais l'appareil.
