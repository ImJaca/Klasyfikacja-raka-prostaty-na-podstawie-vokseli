# Klasyfikacja wokseli raka prostaty przy użyciu sieci neuronowej

Projekt uczenia maszynowego polegający na klasyfikacji wokseli jako zdrowe lub nowotworowe na podstawie cech wyekstrahowanych z obrazów MRI prostaty. Celem projektu było stworzenie modelu zdolnego do automatycznego wykrywania zmian nowotworowych w strefie obwodowej prostaty.

## Technologie
- Python
- NumPy
- Scikit-learn
- TensorFlow / Keras
- Matplotlib
- PCA

## Pipeline przetwarzania danych

```mermaid
flowchart LR
A[Surowe cechy wokseli] --> B[Balansowanie danych dla pacjentów]
B --> C[Podział danych GroupShuffleSplit]
C --> D[Standaryzacja StandardScaler]
D --> E[Redukcja wymiarowości PCA]
E --> F[Sieć neuronowa]
F --> G[Predykcja: zdrowy / nowotwór]
```

Najważniejsze kroki przetwarzania danych:
- balansowanie danych aby każdy pacjent posiadał tyle samo zdrowych co chorych wokseli
- podział danych z uwzględnieniem identyfikatora pacjenta (GroupShuffleSplit)
- standaryzacja cech
- redukcja wymiarowości PCA (48 → 10 cech)

## Architektura modelu

```
Input (10 cech po PCA)

Dense(128) + LeakyReLU
Dropout(0.5)

Dense(64) + LeakyReLU
Dropout

Dense(1) + Sigmoid
```

Model wykorzystuje:
- funkcję straty **Binary Crossentropy**
- optymalizator **Adam**
- regularizację **L2**
- **Dropout** w celu ograniczenia overfittingu

## Wyniki modelu

| Metryka | Wynik |
|--------|--------|
| Precision | 0.6673 |
| Recall | 0.8620 |
| ROC AUC | 0.7910 |

Wysoka wartość **Recall** wskazuje na dobrą skuteczność modelu w wykrywaniu wokseli nowotworowych, co jest lepszym rozwiązanie pod kątem zastosowania modelu w medycynie.

## Struktura repozytorium

```
Klasyfikacja-raka-prostaty-na-podstawie-vokseli/
│
├── projekt2.ipynb
├── data/
│   ├── x_data_corrected_pz.npy
│   ├── y_labels_pz.npy
│   └── patient_labels_pz.npy
└── README.md
```

## Autorzy

ImJaca,
Diabii
