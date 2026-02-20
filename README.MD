# INF6083 — Analyse des avis Amazon (Books)

## Structure du projet

```
.
├── amazon-reviews-analysis.ipynb   # Notebook principal (toutes les tâches)
├── requirements.txt                # Dépendances Python (pip)
├── data/                           # Données brutes (à télécharger, voir ci-dessous)
│   ├── Books.jsonl
│   └── meta_Books.jsonl
├── sample-cudf-activ-users/        # Données pré-calculées (échantillon utilisateurs actifs)
│   └── splits/
│       ├── R_train.npz
│       ├── R_test.npz
│       ├── user_ids.npy
│       ├── item_ids.npy
│       └── similarities/
│           ├── sim_cosine.npz
│           ├── sim_jaccard.npz
│           └── sim_pearson.npz
└── sample-cudf-temporal/           # Données pré-calculées (échantillon temporel)
    └── splits/
        └── ...  (même structure)
```

## Prérequis

- **Python** ≥ 3.10
- **pip** (ou conda/mamba)
- Environ **8 Go de RAM** disponibles
- *Optionnel* : GPU NVIDIA avec CUDA pour l'accélération PyTorch

## Installation rapide

### 1. Créer un environnement virtuel

```bash
python -m venv .venv

# Activation :
# Linux / macOS
source .venv/bin/activate
# Windows
.\.venv\Scripts\activate
```

### 2. Installer les dépendances

```bash
pip install -r requirements.txt
```

> **PyTorch avec CUDA** (optionnel, pour accélération GPU) :
> si vous disposez d'un GPU NVIDIA, installez PyTorch avec le support CUDA
> au lieu de la version CPU par défaut. Consultez
> [pytorch.org/get-started](https://pytorch.org/get-started/locally/)
> pour la commande adaptée à votre configuration.
> Exemple (CUDA 12.4) :
> ```bash
> pip install torch --index-url https://download.pytorch.org/whl/cu124
> ```

### 3. Données

#### Option A — Données pré-calculées (recommandé pour l'évaluation)

Les dossiers `sample-cudf-activ-users/` et `sample-cudf-temporal/` contiennent
les matrices d'entraînement/test et les matrices de similarité pré-calculées.
**Si ces dossiers sont fournis avec le projet, aucune donnée brute n'est
nécessaire** : le notebook peut être exécuté directement à partir de la
Tâche 1 (les cellules d'échantillonnage GPU seront automatiquement ignorées).

#### Option B — Depuis les données brutes

1. Télécharger le dataset *Amazon Reviews 2023* (Books) :
   - Reviews : [mcauleylab.ucsd.edu](https://mcauleylab.ucsd.edu/public_datasets/data/amazon_2023/raw/review_categories/Books.jsonl.gz)
     — Miroir : [huggingface.co](https://huggingface.co/datasets/McAuley-Lab/Amazon-Reviews-2023/blob/main/raw/review_categories/Books.jsonl)
   - Metadata : [mcauleylab.ucsd.edu](https://mcauleylab.ucsd.edu/public_datasets/data/amazon_2023/raw/meta_categories/meta_Books.jsonl.gz)
     — Miroir : [huggingface.co](https://huggingface.co/datasets/McAuley-Lab/Amazon-Reviews-2023/blob/main/raw/meta_categories/meta_Books.jsonl)

2. Décompresser et placer les fichiers dans `data/` :
   ```
   data/Books.jsonl
   data/meta_Books.jsonl
   ```

3. **RAPIDS requis** : les cellules d'échantillonnage (Tâche 0) utilisent
   cuDF/cuPy/RMM pour le traitement GPU. Installer via conda :
   ```bash
   conda install -c rapidsai -c conda-forge cudf cupy rmm
   ```

### 4. Lancer le notebook

```bash
# Via Jupyter
pip install notebook
jupyter notebook amazon-reviews-analysis.ipynb

# Ou via VS Code avec l'extension Jupyter
# https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter
```

## Notes techniques

- **RAPIDS (cuDF/cuPy/RMM)** n'est nécessaire que pour les cellules
  d'échantillonnage initial (Tâche 0). Si ces bibliothèques ne sont pas
  installées, les cellules concernées sont automatiquement ignorées.
- **PyTorch** est utilisé pour l'accélération GPU dans les tâches 3 à 5
  (K-Means, PCA). Si CUDA n'est pas disponible, le notebook bascule
  automatiquement sur les implémentations CPU (scikit-learn).
- Le notebook a été développé et testé sous Arch Linux avec Python 3.14,
  mais devrait fonctionner avec Python ≥ 3.10.
