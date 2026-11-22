# S&P 500 Stock Analysis Using RFM and Clustering

## About This Project

In this project, I analysed S&P 500 stocks using
historical stock market data from 2021 to 2024.

My aim was to group stocks based on their weekly
returns, market risk and trading activity.

I used two sets of features:
- Average weekly return and weekly beta
- Recency, Frequency and Monetary (RFM)

I used K-means and Ward hierarchical clustering
to compare how the stocks were grouped.

## Data Sources

I collected the S&P 500 company list from Wikipedia
on 12 November 2026.

Source:
https://en.wikipedia.org/wiki/List_of_S%26P_500_companies

I downloaded daily stock prices and trading volumes
from Yahoo Finance using the yfinance library.

The study period was from 1 January 2021 to
31 December 2024.

I used the S&P 500 index (^GSPC) as the benchmark.

## Data Preparation

I started with 503 stock symbols.

Five symbols did not return usable data:
FDXF, HONA, Q, SNDK and VYLR.

I removed another three stocks because they had
fewer than 52 aligned weekly returns:
GEV, RDDT and SOLV.

This left 495 stocks for the final analysis.

I checked the data for duplicate dates, missing
values, invalid prices and unusual trading volumes.

I used adjusted closing prices to calculate
weekly returns and beta.

## Feature Calculations

### Average Weekly Return

I used Friday-ending weekly adjusted closing prices
to calculate weekly returns.

I then calculated the average weekly return
for each stock.

### Weekly Beta

I calculated weekly beta by comparing each stock's
weekly returns with the S&P 500 index.

### Recency

Recency is the number of calendar days since the
most recent high-volume trading event.

I identified a high-volume event when the daily
volume was more than twice the average volume
of the previous 20 trading sessions.

### Frequency

Frequency is the number of high-volume events
during the final 60 trading sessions.

### Monetary

Monetary is the total estimated trading value
during the final 60 trading sessions.

I calculated this using the closing price
multiplied by the daily trading volume.

This value does not represent company profit
or market capitalisation.

The RFM observation date was 31 December 2024.

## Clustering Methods

I used two separate feature sets:
- Average weekly return and weekly beta
- Recency, Frequency and Monetary

I applied a log transformation to Monetary
because its values were highly skewed.

I standardised the features before clustering.

I used K-means and Ward hierarchical clustering.

I tested cluster numbers from 2 to 8.

I compared silhouette scores, cluster sizes
and average feature values.

I selected two clusters for the main comparisons.

## Main Results

### Return and Beta Clustering

K-means divided the 495 stocks into two groups.

Cluster 0 contained 349 stocks.
Cluster 1 contained 146 stocks.

Cluster 0 had lower average weekly returns
and lower beta values than Cluster 1.

### RFM Clustering

K-means divided the stocks into two groups.

Cluster 0 contained 423 stocks.
Cluster 1 contained 72 stocks.

Cluster 0 had more recent high-volume events
and a higher average event frequency.

Cluster 1 had less recent high-volume events
and a lower average event frequency.

### Comparing the Methods

I compared K-means and Ward clustering
using the adjusted Rand index.

I also tested Ward clustering without Monetary
to see whether the RFM groups changed.

Most stock assignments stayed the same.

I also compared the sectors represented
in the RFM clusters.

## Limitations

I used the S&P 500 company list from November 2026
to study the period from 2021 to 2024.

This creates survivorship bias because the list
does not show the exact companies in the index
during each historical year.

Some stocks had shorter trading histories.

Some historical trading volumes were unusual.
For example, SW had 424 zero-volume records.

Monetary is only an estimate of trading value.

The clusters describe past market behaviour.
They do not predict future stock performance.

## Project Files

- CW1-CRnCM-SP500_RFM_Analysis.ipynb
  Contains the Python analysis and charts.

- sp500_companies.csv
  Contains the S&P 500 company list.

- sp500_raw_data.pkl
  Contains the downloaded historical stock data.

- sp500_final_features.csv
  Contains the final features and cluster results.

- sp500_exclusion_log.csv
  Contains the excluded stocks and reasons.

- requirements.txt
  Lists the Python libraries used.

## How to Run the Project

1. Open the notebook in Google Colab.
2. Install the libraries listed in requirements.txt.
3. Run the notebook cells in order.
4. Review the calculated features and clustering results.

The notebook downloads historical stock data from Yahoo Finance
using yfinance. A new download may return different results
or unavailable symbols.

The file sp500_raw_data.pkl contains the original downloaded
data used for this analysis. It is included as a historical
snapshot to support reproducibility.

The original S&P 500 company list was collected from Wikipedia
on 12 November 2026.

A fresh-run test was completed on 22 November 2026 using
a separate Google Colab environment. The test successfully
executed the analysis and reproduced the main clustering results.

Only load pickle files from trusted sources.

## Software Used

- Python 3.13.18
- Pandas 2.2.3
- NumPy 2.4.6
- yfinance 0.2.66
- Scikit-learn 1.6.1
- SciPy 1.16.3
- Matplotlib 3.10.0
