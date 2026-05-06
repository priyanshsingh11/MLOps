# Building Pipeline

1. Create a GitHub repo and clone it locally (add experiments).
2. Add the `src` folder along with all components (run them individually).
3. Add `data`, `models`, and `reports` directories to the `.gitignore` file.
4. Now do:

```bash
git add .
git commit -m "initial pipeline setup"
git push
```

---

# Setting up DVC Pipeline (Without Params)

5. Create the `dvc.yaml` file and add stages to it.
6. Run:

```bash
dvc init
dvc repro
```

Use the following to check the pipeline DAG:

```bash
dvc dag
```

7. Now do:

```bash
git add .
git commit -m "setup dvc pipeline"
git push
```

---

# Setting up DVC Pipeline (With Params)

8. Add the `params.yaml` file.
9. Add the params setup code.
10. Run again:

```bash
dvc repro
```

This tests the pipeline along with parameters.

11. Now do:

```bash
git add .
git commit -m "added params pipeline"
git push
```

---

# Experiments with DVC

12. Install dvclive:

```bash
pip install dvclive
```

13. Add the `dvclive` code block.
14. Run:

```bash
dvc exp run
```

This will:

* Create a new `dvc.yaml` (if not already present)
* Create a `dvclive` directory
* Treat each run as a separate experiment

15. View experiments:

```bash
dvc exp show
```

Or install the DVC extension in VS Code.

16. Remove or apply experiments:

```bash
dvc exp remove {exp-name}
dvc exp apply {exp-name}
```

17. Change parameters and rerun code to generate new experiments.

18. Finally:

```bash
git add .
git commit -m "added dvc experiments"
git push
```

---

# Adding a Remote S3 Storage to DVC

19. Login to AWS Console.
20. Create an IAM user.
21. Create an S3 bucket (use a unique name).
22. Install dependencies:

```bash
pip install dvc[s3]
pip install awscli
```

23. Configure AWS:

```bash
aws configure
```

24. Add remote storage:

```bash
dvc remote add -d dvcstore s3://bucketname
```

25. Push experiment outputs you want to keep:

```bash
dvc commit
dvc push
```

26. Finally:

```bash
git add .
git commit -m "added s3 remote storage"
git push
```

---

# Extra

## Remove/Delete AWS Resources

Clean up unused AWS resources to avoid unnecessary charges.

## Adding Stage to `dvc.yaml`

```bash
dvc stage add -n data_ingestion -d src/data_ingestion.py -o data/raw python src/data_ingestion.py
```

---

# params.yaml Setup

## 1. Import YAML

```python
import yaml
```

## 2. Add Function

```python
def load_params(params_path: str) -> dict:
    """Load parameters from a YAML file."""
    try:
        with open(params_path, 'r') as file:
            params = yaml.safe_load(file)
        logger.debug('Parameters retrieved from %s', params_path)
        return params
    except FileNotFoundError:
        logger.error('File not found: %s', params_path)
        raise
    except yaml.YAMLError as e:
        logger.error('YAML error: %s', e)
        raise
    except Exception as e:
        logger.error('Unexpected error: %s', e)
        raise
```

## 3. Add to `main()`

### data_ingestion

```python
params = load_params(params_path='params.yaml')
test_size = params['data_ingestion']['test_size']
```

### feature_engineering

```python
params = load_params(params_path='params.yaml')
max_features = params['feature_engineering']['max_features']
```

### model_building

```python
params = load_params('params.yaml')['model_building']
```

---

# dvclive Code Block

## 1. Import dvclive and yaml

```python
from dvclive import Live
import yaml
```

## 2. Add the `load_params` function and initialize `params` variable in `main()`

## 3. Add Below Code Block to `main()`

```python
with Live(save_dvc_exp=True) as live:
    live.log_metric('accuracy', accuracy_score(y_test, y_test))
    live.log_metric('precision', precision_score(y_test, y_test))
    liv
```
