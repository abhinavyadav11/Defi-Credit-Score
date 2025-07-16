# DeFi Credit Score Analysis

This project analyzes DeFi wallet transactions to compute and visualize credit scores for user wallets based on their on-chain activity. The workflow includes data extraction, feature engineering, credit score calculation, and visualization of score distributions.

## Project Structure

- `user-wallet-transactions.json`: Raw transaction data for user wallets.
- `transactions-data.csv`: CSV version of the transaction data.
- `batch-transactions-data.csv`: Sample batch of transaction data (first 100 rows).
- `wallet_scores.csv`: Computed credit scores for each wallet.
- `score_distribution.png`: Bar plot showing the distribution of wallets by credit score.
- `data.ipynb`: Jupyter notebook containing the full data processing, feature engineering, scoring, and visualization pipeline.

## Workflow Overview

1. **Data Loading & Cleaning**
   - Load JSON transaction data and convert to CSV.
   - Clean and preprocess the data, extracting relevant features (amount, asset, action, etc.).

2. **Feature Engineering**
   - Aggregate wallet activity (deposits, borrows, repayments, etc.).
   - Compute ratios and activity metrics (e.g., repay-to-borrow ratio, active days).

3. **Credit Score Calculation**
   - Normalize features and apply weighted scoring to generate a raw score.
   - Scale raw scores to a 0-1000 range for credit score assignment.
   - Save results to `wallet_scores.csv`.

4. **Visualization**
   - Bin credit scores into ranges (buckets) and plot the distribution.
   - Save the plot as `score_distribution.png`.

5. **Analysis**
   - Display the number of wallets in each credit score group.
   - Query individual wallet scores as needed.

## Usage

Open `data.ipynb` in Jupyter or VS Code and run the cells sequentially to:
- Process and clean the data
- Engineer features
- Calculate credit scores
- Visualize and analyze the results

## Requirements

- Python 3.x
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn

Install dependencies with:

```bash
pip install pandas numpy scikit-learn matplotlib seaborn
```

## Example: Display Wallets per Credit Score Group

To see the number of wallets in each credit score bucket, run the relevant cell in `data.ipynb`:

```python
import pandas as pd
wallet_scores = pd.read_csv("wallet_scores.csv")
bins = list(range(0, 1101, 100))
labels = [f"{i}-{i+99}" for i in bins[:-1]]
wallet_scores["score_bucket"] = pd.cut(wallet_scores["credit_score"], bins=bins, labels=labels, right=False)
bucket_counts = wallet_scores["score_bucket"].value_counts().sort_index()
print(bucket_counts)
```

---

For questions or improvements, please open an issue or submit a pull request.
