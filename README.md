# ML Model Deployment with Flask and Google Cloud

A small end-to-end example of taking a scikit-learn model from training to a hosted web service: a salary-prediction model served through a **Flask** app and deployed on **Google App Engine** (flexible environment) with **gunicorn**.

## How it works

1. `model.py` trains a linear regression on `hiring.csv` (years of experience, test score, interview score → salary) and saves it to `model.pkl`.
2. `main.py` loads the model and serves:
   - `GET /`: a form (`templates/index.html`) for the three inputs
   - `POST /predict`: runs the model and renders the predicted salary
3. `app.yaml` configures App Engine to run the app with `gunicorn -b :$PORT main:app`.

## Run locally

```bash
git clone https://github.com/saurin1004/ML-model-deployment-using-Flask-and-GCP.git
cd ML-model-deployment-using-Flask-and-GCP

python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt

python model.py      # (re)train and save model.pkl
python main.py       # http://127.0.0.1:5000
```

Enter the three values and click **Predict**.

## Deploy to Google App Engine

Requires the [Google Cloud CLI](https://cloud.google.com/sdk/docs/install) and a GCP project with billing enabled. Cloud Shell works too.

```bash
gcloud config set project <your-project-id>
gcloud app deploy          # uses app.yaml
gcloud app browse          # open the deployed app
```

`app.yaml` pins a single small instance (1 vCPU, 0.5 GB) to keep test costs low. The flexible environment still bills while running, so stop the version when you're done with `gcloud app versions stop <version>`.

## Project structure

| File | Purpose |
| --- | --- |
| `model.py` | Trains the regression model and writes `model.pkl` |
| `main.py` | Flask app (form + `/predict`) |
| `templates/index.html`, `static/css/style.css` | Web UI |
| `hiring.csv` | Training data |
| `app.yaml` | App Engine configuration |
| `requirements.txt` | Python dependencies |

## Tech stack

Python · scikit-learn · pandas · NumPy · Flask · gunicorn · Google App Engine
