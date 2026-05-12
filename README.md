# Market-Sentiment-Analysis
This project aligns historical trading data with the Crypto Fear & Greed Index to analyze how market sentiment influences trader behavior and performance. It identifies key trader segments and proposes sentiment-based trading strategies.

## Project Structure
- `historical_data.csv`: Raw trading history.
- `fear_greed_index.csv`: Daily sentiment index data.
- `analysis.py`: Main Python script for data alignment, EDA, and segmentation.
- `aligned_historical_fg_data.csv`: The processed dataset (Output).
- `plots/`: Directory containing generated analytical charts.
## Setup
pip install pandas numpy matplotlib seaborn
## Output Charts & Tables

#### **Table: Performance Summary by Sentiment**
| Sentiment | Avg PnL | Win Rate | Daily Trade Frequency | L/S Ratio |
| :--- | :--- | :--- | :--- | :--- |
| **Fear** | $49.21 | 84.4% | 792.7 | 0.98 |
| **Greed** | $53.88 | 82.4% | 294.1 | 0.89 |
| **Neutral** | $34.31 | 82.3% | 562.4 | 1.01 |

## **Visual Insights**
### Summary Report (Analysis & Strategy)

#### **Methodology**
The analysis followed a four-step pipeline:
1.  **Data Alignment:** Trading timestamps were normalized to a daily level to merge with the Fear & Greed Index. Missing sentiment values were handled using defensive programming (`pd.isna`).
2.  **Feature Engineering:** Calculated "Realized Win Rate" by filtering for non-zero PnL trades and developed a "Consistency Score" using the Coefficient of Variation ($CV = \sigma / |\mu|$).
3.  **Behavioral Analysis:** Evaluated the Long/Short ratio and trade frequency as a function of the sentiment index.
4.  **Segmentation:** Used median-based binning to categorize 32 accounts into "Consistent Snipers," "Volatile Scalpers," and "High-Risk Gamblers."

#### **Key Insights**
* **The Fear Paradox:** Trading frequency is **2.7x higher** during Fear days than Greed days. While traders trade more often and win more frequently (84.4% win rate) during Fear, their average profit per trade is lower than during Greed.
* **Contrarian Sentiment:** There is a clear "Sell the Greed" bias. The Long/Short ratio drops to **0.89** as the market moves into Greed, indicating that the cohort of traders analyzed predominantly attempts to short market tops.
* **Volatility Clusters:** Risk (PnL Std Dev) is nearly **double** in Fear/Greed states compared to Neutral states, highlighting that sentiment extremes are the primary drivers of drawdown.



#### **Strategy Recommendations**
1.  **Rule of Thumb (Fear):** *The Survival Rule.* For "Frequent Scalper" segments, implement a mandatory **50% leverage reduction** during Fear days. High frequency combined with extreme volatility increases the risk of "ruin" despite a high win rate.
2.  **Rule of Thumb (Greed):** *The Liquidity Exit.* For "Consistent Sniper" segments, increase position sizes for **Short-biased mean-reversion trades** when the index is > 75. Greed periods provide the highest average PnL per trade, making them the optimal environment for high-conviction contrarian bets.
