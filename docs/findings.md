# Findings: Titanic Cleaning and EDA

## Dataset source and description
- Titanic passenger data, 891 rows and 12 columns, from the training file of Kaggle's *Titanic: Machine Learning from Disaster* competition (https://www.kaggle.com/c/titanic/data).
- Each row is one passenger. `Survived` records whether they survived, and the other columns describe the passenger (class, sex, age, family aboard, fare, cabin, port of embarkation).

## Data quality issues found
| Issue | Size | Handling |
|---|---|---|
| Age missing | about 20% of rows | Filled with median age by class and sex |
| Cabin missing | about 77% of rows | Replaced with `HasCabin` flag, column dropped |
| Embarked missing | 2 rows | Filled with the most common port |
| Duplicates / impossible values | checked | Duplicate rows removed if any; no impossible ages or negative fares expected |
| Fare outliers | a few dozen high fares | Flagged with the IQR rule, kept because they are genuine first-class fares |

## Cleaning steps performed
1. Copied the raw data so the original stays untouched.
2. Removed duplicate rows.
3. Standardised text in Sex and Embarked.
4. Filled missing Embarked, Age and Fare values (methods above).
5. Replaced Cabin with a HasCabin flag.
6. Created Title (from Name), FamilySize, IsAlone, AgeGroup and a readable Survival label.
7. Dropped Name and Ticket.
8. Set category data types and confirmed no missing values remain.
9. Saved the result to `data/titanic_cleaned.csv`.

## Key observations from EDA
1. About 38% of passengers survived.
2. **Sex** is the strongest pattern: women survived at roughly 74% and men at roughly 19%.
3. **Class** matters: survival was roughly 63% in 1st class, 47% in 2nd and 24% in 3rd.
4. Women in 1st and 2nd class almost all survived, while men in 3rd class fared worst.
5. Children survived more often than adults, and the oldest passengers did worst.
6. Small families (2 to 4 people) did better than people travelling alone or in very large families.
7. Passengers who embarked at Cherbourg survived more often than those from Southampton, partly because more of them travelled first class.
8. Passengers with a recorded cabin survived more often, which mostly reflects higher class.
9. Fares are strongly right-skewed and rise sharply with class.

## Limitations
- Imputed ages are estimates, so age-based findings are less certain.
- Patterns shown are associations, not proof of cause (for example, class and cabin overlap).

## Charts
All charts are saved in the `images/` folder: missing values, survival counts, distributions, survival by group, survival by sex and class, age and fare by class, and the correlation heatmap.
