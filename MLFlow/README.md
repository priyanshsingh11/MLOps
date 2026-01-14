# MLflow – Experiment Tracking & Model Lifecycle Management

MLflow is an open-source platform used to **track ML experiments, manage models, and support reproducibility** across the ML lifecycle. It is widely used in MLOps pipelines to move from experimentation to production.

---

## Why MLflow is Used

- Track experiments (parameters, metrics, artifacts)
- Compare multiple model runs easily
- Store and version trained models
- Support reproducible ML workflows
- Integrate with most ML frameworks (PyTorch, TensorFlow, Scikit-learn, XGBoost)

---

## Core MLflow Components

### 1. Tracking
Logs:
- Parameters
- Metrics
- Artifacts (models, plots, files)

### 2. Projects
Standard way to package ML code for reproducible runs.

### 3. Models
Unified model format that supports multiple deployment targets.

### 4. Model Registry
Centralized model store with versioning and stage transitions (Staging, Production).

---

## Common MLflow Commands

```bash
mlflow ui
mlflow run .
mlflow models serve -m runs:/<run_id>/model
