# Solutions pour l'erreur LightGBM "OSError: access violation"

## Solution 1 : Convertir explicitement en arrays numpy contiguës
```python
# Avant l'entraînement LightGBM, ajoutez cette cellule:
# Conversion en numpy arrays contiguës pour éviter les problèmes de mémoire
X = pd.DataFrame(np.ascontiguousarray(X.values), columns=X.columns, index=X.index)
X_test = pd.DataFrame(np.ascontiguousarray(X_test.values), columns=X_test.columns, index=X_test.index)
print("✅ Données converties en arrays contiguës")
```

## Solution 2 : Réduire la taille du dataset temporairement
```python
# Pour tester, utiliser un sous-échantillon
sample_size = 1000000  # 1 million de lignes
idx = np.random.choice(len(X), size=min(sample_size, len(X)), replace=False)
X_sample = X.iloc[idx].reset_index(drop=True)
y_sample = y[idx]
```

## Solution 3 : Utiliser l'API sklearn de LightGBM
```python
from lightgbm import LGBMClassifier

# Remplacer la section LightGBM par:
model = LGBMClassifier(
    **lgb_params,
    n_estimators=1000,
    early_stopping_round=50
)
model.fit(
    X_train, y_train,
    eval_set=[(X_val, y_val)],
    eval_metric='auc'
)
oof_preds[val_idx] = model.predict_proba(X_val)[:, 1]
```

## Solution 4 : Réinstaller LightGBM
```bash
pip uninstall lightgbm -y
pip install lightgbm --no-binary lightgbm
```
