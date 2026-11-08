# SprintLab

Application web (un seul fichier `index.html`, aucune dépendance) pour mesurer, analyser et faire progresser la vitesse des sprinteurs. Ouvrez `index.html` dans un navigateur, sur ordinateur ou sur téléphone.

## Onglets

- **Équipe** : classement par vitesse max, 30 m projeté, tendance par athlète, fiche de progression, ajout d'athlètes, export/import JSON.
- **Chrono** : saisie des temps de passage (gabarits 20/30/60/100 m). Calcule la vitesse par segment et ajuste le modèle
  `v(t) = Vmax·(1 − e^(−t/τ))` : Vmax, τ, accélération initiale, distance à 95 % de Vmax.
- **Modèle** :
  - *Prédicteur* : 100 m prédit (avec fourchette), passages 30/60 m et prochain palier à partir d'une séance, d'une vitesse max ou d'un 10 m lancé ; classement prédit de toute l'équipe.
  - *Objectif → vitesse requise* : course modèle 100 m pour un objectif de temps (réaction, τ, perte de vitesse en fin de course) :
  vitesse max requise, temps de passage tous les 10 m, courbes des temps voisins, comparaison avec une séance enregistrée.
- **Vidéo** : suivi automatique du squelette par IA (MediaPipe Pose, exécuté sur l'appareil) :
  - angles en direct sur la vidéo (genoux, hanches, tronc, coudes) et courbes des angles au fil du temps ;
  - détection automatique des appuis : temps de contact, temps de vol, fréquence, longueur de pas, vitesse ;
  - affichage des appuis et des longueurs de pas directement sur l'image (caméra fixe) ;
  - étalonnage par la taille de l'athlète ou par 2 repères au sol ; caméra qui suit l'athlète : longueur = vitesse × temps de pas ;
  - prise en charge des ralentis (2×/4×/8×), lecture image par image, mesures manuelles (angle, inclinaison, chrono).

  Le modèle (≈ 10 Mo) est chargé depuis cdn.jsdelivr.net à la première analyse ; une connexion internet est donc nécessaire la première fois.

Les données sont stockées dans le navigateur (`localStorage`) ; les vidéos ne quittent jamais l'appareil.
