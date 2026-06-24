# Loan Default Prediction

End-to-end machine learning system for predicting the probability of loan default, built on the LendingClub public dataset. Covers the full lifecycle: data versioning, feature engineering, model training and tuning, explainability, REST API, containerization, and CI/CD.

> **Status:** 🚧 Phase 1 of 8 — project scaffolding. See [Roadmap](#roadmap) for what's shipped and what's next.

---

## Problem

Consumer lending platforms approve or reject loan applications under uncertainty: a fraction of approved borrowers will default, and the cost of a false approval is far higher than the cost of a false rejection. Lenders need calibrated probability estimates — not just yes/no predictions — to price risk, set credit limits, and meet regulatory explainability requirements.

This project builds and serves a default-risk model on the LendingClub dataset (2007–2018, ~2.2M loans), with the production concerns a real lender would care about: leakage-free features, class-imbalance handling, threshold tuning for asymmetric costs, SHAP-based explanations per prediction, and a deployed inference API.

## Results

> Coming in Phase 5. Target metrics: ROC-AUC ≥ 0.72, PR-AUC ≥ 0.45, expected-cost reduction vs. naive baseline reported.

A `MODEL_CARD.md` will document performance, limitations, fairness considerations, and intended use (Phase 6).

## Tech Stack

| Layer | Tools |
|---|---|
| Data | pandas, polars, pyarrow, DVC |
| Modeling | scikit-learn, LightGBM, Optuna, imbalanced-learn |
| Explainability | SHAP |
| Tracking | MLflow |
| Serving | FastAPI, Pydantic, Uvicorn |
| Demo UI | Streamlit |
| Packaging | Docker |
| CI/CD | GitHub Actions |
| Quality | Ruff, pytest, pre-commit |

## Architecture

> Diagram coming in Phase 7. High-level flow: raw data → DVC-tracked snapshots → preprocessing pipeline → LightGBM model → MLflow registry → FastAPI service → Docker container → CI/CD → live endpoint.

## Roadmap

- [x] **Phase 1 — Scaffolding:** repo, venv, tooling, pre-commit, CI skeleton
- [ ] **Phase 2 — Data & EDA:** DVC setup, LendingClub ingestion, leakage audit, EDA notebooks
- [ ] **Phase 3 — Feature engineering:** preprocessing pipelines, encoding, train/val/test splits with temporal awareness
- [ ] **Phase 4 — Baseline:** logistic regression with class weights, calibration check
- [ ] **Phase 5 — Main model:** LightGBM + Optuna tuning + threshold optimization, MLflow tracked
- [ ] **Phase 6 — Explainability:** SHAP global and local explanations, MODEL_CARD.md
- [ ] **Phase 7 — Serving:** FastAPI service, Pydantic schemas, Dockerfile, local integration tests
- [ ] **Phase 8 — Deploy & demo:** GitHub Actions CI/CD, Render or HF Spaces deployment, Streamlit demo

## Live Demo

> Coming in Phase 8.

## Getting Started

### Prerequisites

- Python 3.11+
- Git
- (Optional) Docker, for running the API container locally

### Setup

​```bash
git clone https://github.com/ikur0/loan-default-prediction.git
cd loan-default-prediction
python -m venv .venv
.venv\Scripts\activate          # Windows
source .venv/bin/activate       # macOS/Linux
pip install -r requirements.txt
​```

### Development

​```bash
ruff check .                    # lint
ruff format .                   # format
pytest                          # run tests
​```

Pre-commit hooks run `ruff` automatically on staged files:

​```bash
pre-commit install
​```

## Project Structure

​```
loan-default-prediction/
├── .github/                    # CI workflows
├── notebooks/                  # EDA and modeling experiments
├── src/
│   ├── api/                    # FastAPI serving layer
│   ├── data/                   # ingestion, validation, splits
│   ├── evaluation/             # metrics, calibration, model card
│   ├── models/                 # training, inference, registry
│   └── streamlit_app/          # interactive demo UI
├── tests/                      # pytest suite
├── data/                       # DVC-tracked (not committed)
├── models/                     # DVC-tracked artifacts (not committed)
├── .gitignore
├── .pre-commit-config.yaml
├── LICENSE
├── pyproject.toml              # ruff, pytest config
├── README.md
└── requirements.txt            # pinned dependencies
​```

## License

MIT — see [`LICENSE`](LICENSE).

## Author

**Khalid Almutairi** — final-year CS, Qassim University.
[GitHub](https://github.com/ikur0) · [LinkedIn](https://linkedin.com/in/khalidmutlaqalmutairi/)
