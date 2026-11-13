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
  - repérage automatique de l'athlète par le mouvement (caméra fixe), ou ciblage manuel ; un athlète petit ou loin
    est suivi dans une zone agrandie, recherchée à plusieurs échelles ;
  - nettoyage des trajectoires : correction des inversions gauche/droite, suppression des points aberrants, lissage ;
  - angles en direct sur la vidéo (genoux, hanches, chevilles, tronc, coudes) et courbes des angles au fil du temps ;
  - alignement en milieu d'appui : inclinaison du tronc et de l'axe de la jambe d'appui (cheville → hanche), et
    « cassure aux hanches » = tronc − axe (0° = corps aligné depuis le pied, positive = tronc qui plonge en avant) ;
  - cheville : dorsiflexion = 90° − angle tibia/pied (talon → pointe), positive pointe relevée, négative en flexion
    plantaire ; dorsiflexion maximale pendant chaque appui ;
  - appuis : temps de contact et de vol (ralenti ≥ 100 i/s et athlète assez grand à l'image), fréquence, longueur de pas,
    vitesse et courbe de vitesse au fil du temps ;
  - longueur de chaque pas par les « empreintes » (positions des pieds plantés), même quand les temps de contact ne sont
    pas mesurables ; pas douteux signalés ; méthode de secours par le rythme des jambes à 30 i/s ;
  - garde-fous : temps de contact masqués s'ils ne sont pas fiables, suggestion du facteur de ralenti si la fréquence
    mesurée est impossible ;
  - étalonnage par la taille de l'athlète ou par 2 repères au sol ; caméra qui suit l'athlète : longueur = vitesse × temps de pas ;
  - prise en charge des ralentis (2×/4×/8×), lecture image par image, mesures manuelles (angle, inclinaison, chrono).

  Conseils de tournage : caméra fixe, de profil, athlète d'au moins un tiers de la hauteur de l'image, ralenti 120 ou
  240 i/s, deux plots à distance connue (de centre à centre) dans le champ.

  Le modèle (≈ 28 Mo en précision « Précise », par défaut ; 3 à 7 Mo en « Rapide » ou « Standard ») est chargé depuis
  cdn.jsdelivr.net à la première analyse ; une connexion internet est donc nécessaire la première fois.

Les données sont stockées dans le navigateur (`localStorage`) ; les vidéos ne quittent jamais l'appareil.
