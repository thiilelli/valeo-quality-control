# Valeo Quality Control — Computer Vision Challenge

Solution Computer Vision pour le challenge ENS Data **"Amélioration du contrôle qualité industriel"** proposé par Valeo.

## 🎯 Objectif

Automatiser la détection de défauts sur chaînes de production Valeo à partir d'images industrielles :

1. **Classification** des pièces en 6 catégories (1 GOOD + 5 défauts)
2. **Détection d'anomalies** hors distribution (classe "drift")

La difficulté principale : un fort déséquilibre de classes et la nécessité de détecter des images de types jamais vus en entraînement (drift), pénalisées lourdement par la matrice de coût du challenge.

## 📊 Dataset

- **Train** : 8 278 images (6 classes, PNG grayscale)
- **Test** : 1 055 images (7 classes, incluant `drift`)
- **Métadonnées** : `lib` (composant, 4 valeurs) × `window` (zone, 2 valeurs)
- **Résolutions** : 540×630 (53%) ou 720×840 (47%)

### Distribution des classes (train)

| Classe | Count | % |
|--------|-------|---|
| Missing | 6 472 | 78.2% |
| GOOD | 1 235 | 14.9% |
| Lift-off blanc | 270 | 3.3% |
| Short circuit MOS | 126 | 1.5% |
| Lift-off noir | 104 | 1.3% |
| Boucle plate | 71 | 0.9% |

Ratio de déséquilibre : **91:1**

## 🏗️ Structure du projet

```text
valeo-quality-control/
├── notebooks/
│   └── 01_eda.ipynb
├── docs/
│   └── eda_findings.md
├── requirements.txt
├── .gitignore
└── README.md
```

## 🚀 Setup

### Prérequis

- Python 3.10+
- GPU recommandé (CUDA)

### Installation

```bash
git clone https://github.com/USERNAME/valeo-quality-control.git
cd valeo-quality-control
pip install -r requirements.txt
```

## Données

Les données ne sont pas versionnées. Pour les obtenir :

- Télécharger le dataset depuis le challenge ENS Data.
- Placer les fichiers dans un dossier `data/` ou monter Google Drive si Colab.
- Adapter le chemin `DATA_ROOT` dans le premier notebook.

## 📓 Notebooks

| Notebook | Contenu | Statut |
|---|---|---|
| `01_eda.ipynb` | Exploration des données, statistiques, visualisations | ✅ Terminé |
| `02_baseline.ipynb` | Baseline classifier (EfficientNet-B0) | 🚧 En cours |
| `03_anomaly.ipynb` | Anomaly detection (PADIM) | ⏳ À venir |
| `04_final.ipynb` | Pipeline complet + évaluation | ⏳ À venir |

## 🎯 Stratégie

### Pipeline cible

```text
Image → Rotate + Crop → Classifier (6 classes)
                     ↓                ↓
                Anomaly Detector → Fusion → Classe finale (0-6)
```

### Choix techniques (planifiés)

- Backbone : EfficientNet-B0 (baseline), ResNet50, ConvNeXt-Tiny
- Loss : Focal Loss (déséquilibre extrême)
- Anomaly : PADIM ou PatchCore
- Validation : K-fold stratifié par `(Label, lib, window)`
- Métrique : Score custom Valeo (matrice de coût)

## 📈 Résultats

Baseline model trained: val Valeo cost = 911


- Focal Loss : Lin et al., 2017

## 📝 Licence

MIT
