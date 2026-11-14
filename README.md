# Titanic: Data Collection, Cleaning & Exploratory Data Analysis

An end-to-end beginner data analysis: load a raw real-world dataset, check its quality, clean it, and explore it with statistics and charts to find what influenced survival on the Titanic.

## Dataset
- **Name:** Titanic passenger data (891 passengers, 12 columns)
- **Source:** the training file (`train.csv`) of Kaggle's *Titanic: Machine Learning from Disaster* competition: https://www.kaggle.com/c/titanic/data
- **Loaded from:** a public CSV copy, https://raw.githubusercontent.com/datasciencedojo/datasets/master/titanic.csv
- **Target of interest:** `Survived` (0 = died, 1 = survived)

See the column descriptions in the notebook and in [docs/findings.md](docs/findings.md).

## What the notebook does
1. **Loads** the raw data and inspects its structure
2. **Checks quality:** missing values, duplicates, impossible or inconsistent values
3. **Cleans** the data (steps listed below) and saves `data/titanic_cleaned.csv`
4. **Explores** it with distributions, survival-rate comparisons, a sex-by-class heatmap, and a correlation matrix
5. **Summarises** the key observations

## Cleaning steps
| Step | Action |
|---|---|
| Duplicates | Removed duplicate rows |
| Text values | Stripped spaces and standardised case in Sex and Embarked |
| Embarked | Filled the missing values with the most common port |
| Age | Filled missing ages with the median age for the passenger's class and sex |
| Fare | Filled any missing fare with the class median |
| Cabin | About 77% missing, so replaced by a `HasCabin` flag and dropped |
| New features | `Title`, `FamilySize`, `IsAlone`, `AgeGroup`, `Survival` |
| Dropped | `Name` and `Ticket` (identifiers) |
| Outliers | High fares flagged with the IQR rule but kept (real values) |

## How to run
```bash
git clone <this-repo-url>
cd <repo-folder>
pip install -r requirements.txt
jupyter notebook notebooks/titanic_eda.ipynb
```
Run all cells from top to bottom. The notebook downloads the data if `data/titanic.csv` is not present, and saves charts to `images/`. It also works in Google Colab.

## Structure
```
README.md
requirements.txt
notebooks/titanic_eda.ipynb
data/titanic.csv            (raw data)
data/titanic_cleaned.csv    (cleaned data)
docs/findings.md
images/                     (saved charts)
```

## Key observations
See [docs/findings.md](docs/findings.md) for the full write-up.
