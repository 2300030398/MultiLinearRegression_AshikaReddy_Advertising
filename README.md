# Sales Prediction using Multiple Linear Regression

A machine learning project that predicts product sales from advertising spend on TV, Radio and Newspaper, using the Advertising dataset and Multiple Linear Regression.

## Business Problem

A company sells a consumer product and advertises on three channels: TV, Radio and Newspaper. The question this project answers is: if we know how much is spent on each channel, can we estimate sales?

## Dataset

- **Source:** Advertising dataset (`Advertising.csv`)
- **Size:** 200 rows, 4 columns
- **Columns:**
  - `TV`: advertising spend on TV (in thousands)
  - `Radio`: advertising spend on Radio (in thousands)
  - `Newspaper`: advertising spend on Newspaper (in thousands)
  - `Sales`: units sold (in thousands)
- **Data quality:** No missing values, so no cleaning was required.

## Tech Stack

- Python
- Pandas
- scikit-learn
- Matplotlib

## Project Workflow

1. **Load and inspect the data:** Checked the shape, data types and missing values.
2. **Select features and target:** Inputs are TV, Radio and Newspaper. The target is Sales.
3. **Train/test split:** 80:20 split (160 training rows, 40 testing rows) with `random_state=42`.
4. **Model training:** Trained a Multiple Linear Regression model, since sales depends on three inputs.
5. **Prediction:** Predicted sales on the unseen test set and compared actual and predicted values, including an error column (Actual - Predicted).
6. **Evaluation:** Measured performance with MAE, MSE, RMSE and R2.
7. **Coefficient analysis:** Interpreted how each channel affects sales.
8. **Visualization:** Plotted actual vs predicted sales.
9. **Business recommendation:** Turned the findings into budget advice.

## Results

Approximate results on the test set (`random_state=42`). Exact values may vary slightly with a different split.

| Metric | Value |
|---|---|
| MAE | about 1.5 |
| MSE | about 3.2 |
| RMSE | about 1.8 |
| R2 | about 0.90 |

- On average, predictions are off by roughly 1.5 thousand units (MAE).
- An R2 of about 0.90 means the model explains around 90% of the variation in sales on the test data.

### Model Coefficients (approximate)

| Feature | Coefficient |
|---|---|
| Intercept | 2.98 |
| TV | 0.045 |
| Radio | 0.189 |
| Newspaper | 0.003 |

- **TV:** Each extra unit of TV spend adds about 0.045 units of sales, with the other budgets held constant.
- **Radio:** Each extra unit of Radio spend adds about 0.189 units of sales. Radio shows the strongest effect.
- **Newspaper:** The coefficient is close to zero, so it adds almost nothing once TV and Radio are included.

Coefficient size alone is not a perfect way to rank channels, because each channel has a different cost and spending range. Standardized coefficients and cost per unit give a fairer comparison.

### Example Prediction

For a budget of TV = 150, Radio = 20, Newspaper = 30, the model predicts about 13.5 thousand units of sales.

```python
new_budget = pd.DataFrame({"TV": [150], "Radio": [20], "Newspaper": [30]})
print(model.predict(new_budget)[0])
```

## Business Recommendation

Radio shows the strongest effect per unit of spending, so it deserves more attention. Newspaper should not be cut completely based on this model alone. Before changing the budget, the company should check campaign costs, audience reach and profit per channel. A safe approach is to raise the Radio budget slightly, track sales and return on ad spend, and compare the results with existing campaigns.

## How to Run

1. Clone the repository:
   ```bash
   git clone YOUR_REPO_LINK_HERE
   cd YOUR_REPO_NAME
   ```
2. Install the dependencies:
   ```bash
   pip install pandas scikit-learn matplotlib
   ```
3. Place `Advertising.csv` in the project folder and run the notebook or script (`YOUR_FILE_NAME`).

## Future Improvements

- Use cross-validation instead of a single train/test split.
- Try Ridge Regression, Random Forest or Gradient Boosting.
- Check for and handle outliers.
- Test whether the relationship is truly linear, including an interaction effect between TV and Radio.

## Conclusion

Advertising spend is strongly linked to sales. Radio has the strongest effect and Newspaper the weakest. With a test R2 of about 0.90, the model is a good guide, but it should not be the only basis for changing an advertising budget.

## Author

**M.V. Ashika Reddy**
Email: ashikareddymajjiga@gmail.com
