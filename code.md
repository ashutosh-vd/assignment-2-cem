## STATISTICAL ANALYSIS

```python
import pandas as pd

file_path = 'data.csv'
data = pd.read_csv(file_path)

numerical_data = data.select_dtypes(include=['number'])
stats = numerical_data.describe().round(2)

print(stats)
```

## LINE GRAPH AND CORRELATION BETWEEN close price ,VWAP, volume

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

new_df = pd.read_csv('data.csv')

new_df["Date"] = pd.to_datetime(new_df["Date"])

fig, ax1 = plt.subplots(figsize=(14, 8))

color = 'tab:orange'
ax1.set_ylabel('Volume', color=color)
ax1.plot(new_df['Volume'], color=color)
ax1.tick_params(axis='y', labelcolor=color)

ax1.set_xticks([]) 
ax1.set_xlabel('')  

ax2 = ax1.twinx()
color = 'tab:blue'
ax2.set_ylabel('Price (Close & VWAP)', color=color)
ax2.plot(new_df['Close'], color='blue', label='Close')
ax2.plot(new_df['VWAP'], color='green', label='VWAP', linestyle='--')
ax2.tick_params(axis='y', labelcolor=color)

plt.title('Stock Price, Volume, and VWAP over Time')

fig.tight_layout()
fig.legend(loc="upper left", bbox_to_anchor=(0,1), bbox_transform=ax1.transAxes)

plt.show()
```
## LINe PLOT AND CORRELATION BETWEEN turnover and trades

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

new_df = pd.read_csv('data.csv')
new_df["Date"] = pd.to_datetime(new_df["Date"])
new_df = new_df.iloc[867:]

turnover_scale = 10**13
trades_scale = 10**4

fig, ax = plt.subplots(figsize=(10, 6))
ax.set_xticks([])

ax.plot(new_df['Date'], new_df['Turnover'] / turnover_scale, label='Turnover', color='orange')
ax.plot(new_df['Date'], new_df['Trades'] / trades_scale, label='Trades', color='blue')

ax.set_title('Turnover and Trades Over Time')
ax.legend()

ax.set_ylim(0, max(new_df['Turnover'].max() / turnover_scale, new_df['Trades'].max() / trades_scale) * 1.1)

plt.show()

```
