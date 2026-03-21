# 🧠 Youtube Sentiment Analysis

An end-to-end Machine Learning project that performs sentiment analysis on Reddit/YouTube comments, complete with a Flask REST API, DVC pipeline for experiment tracking, MLflow for model management, and a Chrome extension for real-time predictions.

---

## 📁 Project Structure

```
youtube-sentiement-analysis/
├── .dvc/                        # DVC configuration
├── .github/                     # GitHub Actions CI/CD workflows
├── data/                        # Raw and processed datasets
├── flask_api/                   # REST API (app.py)
├── mlruns/                      # MLflow experiment logs
├── notebooks/                   # EDA and model development notebooks
├── src/                         # Source code (pipeline stages)
├── yt-chrome-plugin-frontend/   # Chrome Extension (frontend)
├── dvc.yaml                     # DVC pipeline definition
├── dvc.lock                     # DVC pipeline lock file
├── lgbm_model.pkl               # Trained LightGBM model
├── cicd.yaml                    # CI/CD configuration
├── Dockerfile                   # Docker setup
└── requirements.txt             # Python dependencies
```

---

## ⚙️ Setup & Installation

### 1. Create and Activate Conda Environment

```bash
conda create -n youtube python=3.11 -y
conda activate youtube
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## 🔁 DVC Pipeline

This project uses [DVC](https://dvc.org/) to manage the ML pipeline stages (data ingestion → preprocessing → model training → evaluation).

### Initialize DVC

```bash
dvc init
```

### Reproduce the Full Pipeline

```bash
dvc repro
```

### Visualize the Pipeline DAG

```bash
dvc dag
```

---

## 🚀 Running the Flask API

Start the prediction server:

```bash
python flask_api/app.py
```

The API will be available at `http://localhost:5000`

### API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/predict` | Predict sentiment of comments |
| POST | `/generate_chart` | Generate Pie chart |
| POST | `/generate_trend_graph` | Generate sentiment trend over time |
| POST | `/generate_wordcloud` | Generate word cloud from comments |

### Example Request (Postman / curl)

**POST** `http://localhost:5000/predict`

```json
{
    "comments": [
        "This video is awesome! I loved it a lot",
        "Very bad explanation. Poor video"
    ]
}
```

**Example Response:**

```json
{
    "predictions": ["positive", "negative"]
}
```

---

## 🧪 Experiment Tracking with MLflow

MLflow is used to log metrics, parameters, and model artifacts during training.

To view the MLflow UI:

```bash
mlflow ui
```

Then open `http://localhost:5000` in your browser.

---

## 🐳 Docker

Build and run the project using Docker:

```bash
# Build the image
docker build -t reddit-sentiment-analysis .

# Run the container
docker run -p 5000:5000 reddit-sentiment-analysis
```

---

## 🧩 YouTube Chrome Extension

The project includes a Chrome Extension for real-time YouTube comment sentiment analysis.

### Installation Steps

1. Open Chrome and navigate to:
   ```
   chrome://extensions
   ```

2. Enable **Developer Mode** (toggle in the top-right corner)

3. Click **"Load unpacked"** and select the `yt-chrome-plugin-frontend/` folder

4. The extension will appear in your Chrome toolbar — open a YouTube video and click the extension to analyze comment sentiment in real time

> ⚠️ Make sure the Flask API is running locally before using the extension.

---

## 🔄 CI/CD

This project includes a GitHub Actions CI/CD pipeline configured in `.github/` and `cicd.yaml` for automated testing and deployment.

---

## 📊 Model Details

| Property | Value |
|----------|-------|
| Algorithm | LightGBM (LGBM) |
| Task | Multi-class Sentiment Classification |
| Artifact | `lgbm_model.pkl` |

---

## 📬 Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

---

## 📄 License

This project is licensed under the terms specified in the [LICENSE](LICENSE) file.
