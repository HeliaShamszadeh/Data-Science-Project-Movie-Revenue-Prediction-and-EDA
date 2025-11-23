# 🎬 Movie Analytics & Revenue Prediction

This repository contains a complete data science pipeline on a **movies dataset**, including:
1. **Exploratory Data Analysis (EDA)** of movie production and popularity
2. **Machine Learning models** to predict **box office revenue**

The project was developed as part of a university Data Science course.

---

## ✨ Main Objectives

- Clean and preprocess raw movie metadata
- Explore patterns in:
  - Genres, budgets, runtimes, languages
  - Countries of production
  - Cast & gender distribution of lead roles
- Answer domain questions, such as:
  - Which genres are the most expensive to produce?
  - Which countries invest the most in top genres?
  - Which languages (other than English) appear most often?
  - Which countries tend to produce the longest / shortest movies?
  - How is the gender distribution among the top 5 billed roles?
- Build models to **predict movie revenue** and analyze:
  - Which features matter most for revenue
  - How different regression models compare

---

## 📁 Project Structure

```text
.
├── project.ipynb           # Main notebook: preprocessing, feature engineering, modeling
├── Part2(plots).ipynb      # Additional plots & visualizations
├── Document.pdf            # Full project report (in Persian)
└── README.md               # Project description (this file)
```

> **Note:** The raw CSV datasets are not committed here; place them in the same directory or adjust paths inside the notebooks.

---

## 🧹 Data & Preprocessing

The project works with two main datasets (movies metadata + credits), joined on `id_movie_rt`.
Key steps:

* Remove rows with missing critical values (budget, revenue, runtime, genres, etc.)
* Convert string-encoded lists/dicts (genres, countries, languages, actors, directors) into Python objects
* Extract useful fields such as:
  * `name_genre` (main genre)
  * `name_country` (production countries)
  * `languages`
  * cast and crew names / gender / order
* Create additional features:
  * Log-scaled budget and runtime
  * Genre combinations
  * Number of “famous” actors/directors
  * Interactions (e.g. **budget × runtime**, **audience score × critics score**)
  * Year / decade of release

---

## 🔍 Exploratory Data Analysis (EDA)

Some of the questions explored in the notebooks:

* **Average production budget per genre**
* **Share of each country** in total budget for the **top 5 most expensive genres**
* **Number of movies** over the last 10 years for selected genres (Action, Animation, Sci-Fi)
* **Average runtime by country** (longest/shortest movies)
* **Most frequent languages** (excluding English)
* **Yearly investment in the US film industry** vs. **rest of the world**
* **Gender distribution** of the top 5 billed roles per movie
* **Most popular genres** in the last decade based on:
  * Number of reviews
  * Critics’ scores

Visualization tools:

* `plotly` (interactive plots)
* `matplotlib` (supporting plots / distributions)

---

## 🤖 Modeling

### Target

* `log(revenue)` – logarithm of box office revenue to stabilize variance.

### Features

* Numerical: budget, runtime, scores, counts of reviews, engineered ratios & interactions…
* Categorical: main genre, genre combination, decade, etc. (One-Hot encoded)
* Preprocessing via `ColumnTransformer`:
  * `SimpleImputer` + `StandardScaler` for numerical features
  * `SimpleImputer` + `OneHotEncoder` for categorical features

### Models Compared

* **Linear Regression**
* **Random Forest Regressor**
* **Gradient Boosting Regressor**
* **XGBoost Regressor**

Models are evaluated with **K-Fold Cross-Validation** using:

* Mean Squared Error (MSE)
* R² score

### Model Selection & Hyperparameter Tuning

* The best baseline model (by R²) was **Gradient Boosting Regressor**.
* Hyperparameters tuned with **GridSearchCV**, exploring:
  * `n_estimators`
  * `max_depth`
  * `learning_rate`
* The tuned Gradient Boosting model achieved a **substantial improvement in R²** (≈ 0.86 on the log-revenue target).

Feature importances are also analyzed to identify the most influential factors on revenue.

---

## 🔧 Requirements

Install dependencies (for example via `pip`):

```bash
pip install -r requirements.txt
```

Typical libraries used:

* `python>=3.9`
* `pandas`
* `numpy`
* `plotly`
* `matplotlib`
* `scikit-learn`
* `xgboost`
* `ast` / `literal_eval` utilities

*(Create `requirements.txt` according to your environment if it does not exist yet.)*

---

## 🚀 How to Run

1. Clone the repository:

```bash
git clone [https://github.com/](https://github.com/)<your-username>/<your-repo>.git
cd <your-repo>
```

2. Create & activate a virtual environment (optional but recommended).

3. Install dependencies:

```bash
pip install -r requirements.txt
```

4. Open the notebooks:

```bash
jupyter notebook
```

Then run:

* `project.ipynb` for the full pipeline (preprocessing + modeling)
* `Part2(plots).ipynb` for extra visualizations

---

## 📊 Results & Insights (Short Summary)

* **Gradient Boosting** with tuned hyperparameters provides the best trade-off between accuracy and generalization.
* Revenue is strongly influenced by:
  * Budget and runtime
  * Genre and genre combinations
  * Critics’ and audience scores
  * Number of reviews
  * Presence of well-known cast & directors
* The analysis also highlights:
  * The dominance of certain countries (e.g. the US & UK) in expensive genres
  * Imbalances in gender representation among lead roles
  * Trends in investment and revenue over time

For full details, check the report: **`Document.pdf`**.

---

## 📜 License


```text
MIT License
```

---

## 🙋‍♀️ Authors

* Zahra Dehghan
* Helia Shams Zadeh

Developed under the supervision of **Dr. Naderi** as a course project in Data Science.
