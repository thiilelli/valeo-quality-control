# EDA Findings — Valeo Quality Control

## Résumé

Dataset d’images industrielles avec fort déséquilibre de classes.

## Points clés

- Classe majoritaire très dominante.
- Métadonnées spatiales équilibrées.
- Certaines classes rares restent difficiles.
- Les images sont brutes, pas encore prétraitées.

## Implications

- Loss pondérée ou Focal Loss.
- Sampling équilibré.
- Augmentations fortes sur les classes rares.
- Validation stratifiée.
