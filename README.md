# Predicting House Prices in Ames, Iowa (Multiple Linear Regression)

A Jupyter Notebook project that explores housing data from Ames, Iowa and builds a multiple linear regression model to predict a home's sale price from its above-ground living area and garage size.

## Project Structure

```
.
├── Linear_Regression_Ames.ipynb   # Jupyter Notebook with the full analysis and model
├── ames.csv                       # Dataset (2,930 rows x 14 columns)
└── README.md
```

## Dataset

The data describes **2,930 residential property sales** in Ames, Iowa between 2006 and 2010, collected by the Ames City Assessor's Office. The original dataset has 81 variables; this version keeps 14 of them:

| Column | Description |
|--------|-------------|
| `Year_Built` | Year the house was originally constructed |
| `Year_Remod_Add` | Year the house was last remodelled |
| `Total_Bsmt_SF` | Total basement area (sq ft) |
| `First_Flr_SF` | First floor size (sq ft) |
| `Second_Flr_SF` | Second floor size (sq ft) |
| `Gr_Liv_Area` | Above-grade living area (sq ft) |
| `Full_Bath` | Number of full above-grade bathrooms |
| `Half_Bath` | Number of half above-grade bathrooms |
| `Bedroom_AbvGr` | Number of above-grade bedrooms |
| `Kitchen_AbvGr` | Number of above-grade kitchens |
| `TotRms_AbvGrd` | Total above-grade rooms (excluding bathrooms) |
| `Fireplaces` | Number of fireplaces |
| `Garage_Area` | Garage size (sq ft) |
| `Sale_Price` | Sale price in dollars (**target variable**) |

**Source:** De Cock, D. (2011). *Ames, Iowa: Alternative to the Boston Housing Data as an End of Semester Regression Project.* Journal of Statistics Education, 19(3).

## What the Notebook Does

1. **Data checks:** confirms there are no missing values and that every column is numeric.
2. **Exploratory analysis:**
   - Histograms of `Sale_Price` (raw and log-transformed), `Gr_Liv_Area` and `Garage_Area`
   - A correlation heatmap of all variables
   - Average sale price by year built
   - Scatter plots with trend lines of each predictor against `Sale_Price`
3. **Modelling:**
   - Uses `Gr_Liv_Area` and `Garage_Area` as the features and `Sale_Price` as the target
   - Splits the data 75% / 25% into training and test sets (`random_state=42`)
   - Fits a `LinearRegression` model from scikit-learn
4. **Evaluation:** MSE, RMSE and R² on the test set, plus an actual-vs-predicted plot and a residual plot.
5. **Interpretation:** explains what each coefficient means in dollar terms.

## Results

**Model equation**

```
Sale_Price = -5,059.45 + 78.69 x Gr_Liv_Area + 141.15 x Garage_Area
```

| Metric | Value |
|--------|-------|
| Training set size | 2,197 homes |
| Test set size | 733 homes |
| RMSE | $51,326 |
| R² | 0.6386 |

**Interpreting the coefficients**

- Each extra square foot of above-ground living area adds about **$78.69** to the predicted price, holding garage area constant.
- Each extra square foot of garage area adds about **$141.15**, holding living area constant.
- The intercept is the baseline prediction when both areas are zero, so it has no real-world meaning on its own.

**Key findings from the exploration**

- Sale prices are right-skewed, ranging from about $12,789 to $755,000, with most homes in the lower price range.
- `Gr_Liv_Area` has the strongest correlation with price (r = 0.71). `Garage_Area` (0.64), `Total_Bsmt_SF` (0.63) and `First_Flr_SF` (0.62) are also strongly related.
- `Bedroom_AbvGr` (0.14) and `Kitchen_AbvGr` (-0.12) have weak relationships with price.
- About 158 homes have no garage.
- More recently built homes generally sell for more.
- The model explains roughly 64% of the variance in sale price.

## Requirements

- Python 3.8 or higher
- Jupyter Notebook or JupyterLab
- numpy
- pandas
- seaborn
- matplotlib
- scikit-learn

## Getting Started

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name>

# 2. (Optional) create a virtual environment
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install numpy pandas seaborn matplotlib scikit-learn jupyter

# 4. Launch the notebook
jupyter notebook Linear_Regression_Ames.ipynb
```

Keep `ames.csv` in the same folder as the notebook, since it is loaded with a relative path. Then run all cells in order (**Kernel > Restart & Run All**).

## Limitations

- **Only two features** are used, so the model leaves about 36% of the variance in price unexplained.
- **An RMSE of about $51,000** means predictions can be well off for individual homes, especially expensive ones. The actual-vs-predicted preview shows the model under-predicting a $409,900 home by over $125,000.
- **Linear regression assumes a straight-line relationship.** Prices are right-skewed and a few very large homes are outliers, which can distort the fit.
- The model has not been tested against other train/test splits or with cross-validation.


## Author

**Siboniso Zikhali**
