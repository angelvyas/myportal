---
title: 'practise'
date: 2026-06-16
draft:  false
featured: false  
description: "networks"
thumbnail: "/posts/exam/images/.png"
featureImage: "/posts/exam/images/.png" 
shareImage: "/posts/exam/images/.png"
author: "Angel Vyas"
tags:
    - general
categories:     
    - general
---

### to generate various visiualization using pandas and matplotlib.
```python
import pandas as pd
import matplotlib.pyplot as plt

# Sample Data
data = {
    'Month': ['Jan', 'Feb', 'Mar', 'Apr', 'May'],
    'Sales': [200, 250, 300, 280, 350],
    'Profit': [20, 30, 40, 35, 50]
}

df = pd.DataFrame(data)

# 1. Line Plot
df.plot(x='Month', y='Sales', kind='line', marker='o')
plt.title('Monthly Sales Trend')
plt.xlabel('Month')
plt.ylabel('Sales')
plt.show()

# 2. Vertical Bar Chart
df.plot(x='Month', y='Sales', kind='bar')
plt.title('Monthly Sales')
plt.xlabel('Month')
plt.ylabel('Sales')
plt.show()

# 3. Horizontal Bar Chart
df.plot(x='Month', y='Sales', kind='barh')
plt.title('Monthly Sales (Horizontal Bar Chart)')
plt.xlabel('Sales')
plt.ylabel('Month')
plt.show()

# 4. Histogram
df['Sales'].plot(kind='hist', bins=5)
plt.title('Sales Distribution')
plt.xlabel('Sales')
plt.ylabel('Frequency')
plt.show()

# 5. Pie Chart
df.set_index('Month')['Sales'].plot(kind='pie', autopct='%1.1f%%')
plt.title('Sales Contribution by Month')
plt.ylabel('')
plt.show()

# 6. Scatter Plot
df.plot(x='Sales', y='Profit', kind='scatter')
plt.title('Sales vs Profit')
plt.xlabel('Sales')
plt.ylabel('Profit')
plt.show()

# 7. Box Plot
df[['Sales', 'Profit']].plot(kind='box')
plt.title('Box Plot of Sales and Profit')
plt.ylabel('Values')
plt.show()
```

### to carry out simple multivariate analysis with a focus on pca and lda.
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.datasets import load_iris
from sklearn.decomposition import PCA
from sklearn.discriminant_analysis import LinearDiscriminantAnalysis

# Load data
iris = load_iris()
X, y = iris.data, iris.target
df = pd.DataFrame(X, columns=iris.feature_names)

# Profile Plot
df.head().T.plot()
plt.title("Profile Plot")
plt.show()

# Correlation Heatmap
sns.heatmap(df.corr(), annot=True)
plt.title("Correlation Heatmap")
plt.show()

# PCA Scree Plot
pca = PCA()
pca.fit(X)
plt.plot(range(1,5), pca.explained_variance_ratio_, marker='o')
plt.title("PCA Scree Plot")
plt.show()

# PCA Scatter Plot
X_pca = PCA(n_components=2).fit_transform(X)
plt.scatter(X_pca[:,0], X_pca[:,1], c=y)
plt.title("PCA Scatter Plot")
plt.show()

# LDA Scatter Plot
X_lda = LinearDiscriminantAnalysis(n_components=2).fit_transform(X, y)
plt.scatter(X_lda[:,0], X_lda[:,1], c=y)
plt.title("LDA Scatter Plot")
plt.show()
```

### financial data analysis using heat map, clustering, histogram.
```python
import yfinance as yf
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats
from sklearn.cluster import KMeans

# --------------------------------------------------
# 1. Load Financial Data
# --------------------------------------------------
data = yf.download("AAPL", start="2020-01-01", end="2021-01-01")
print(data.head())

# --------------------------------------------------
# 2. Data Cleaning
# --------------------------------------------------
data = data.dropna()

# --------------------------------------------------
# 3. Outlier Detection (Z-Score)
# --------------------------------------------------
z = stats.zscore(data['Close'])
data = data[abs(z) < 3]

# --------------------------------------------------
# 4. Line Chart
# --------------------------------------------------
plt.plot(data.index, data['Close'])
plt.title("Apple Closing Price")
plt.show()

# --------------------------------------------------
# 5. Histogram
# --------------------------------------------------
plt.hist(data['Close'], bins=20)
plt.title("Histogram of Closing Price")
plt.show()

# --------------------------------------------------
# 6. Correlation Heatmap
# --------------------------------------------------
sns.heatmap(data.corr(), annot=True)
plt.title("Correlation Heatmap")
plt.show()

# --------------------------------------------------
# 7. Descriptive Statistics
# --------------------------------------------------
print(data.describe())

# --------------------------------------------------
# 8. Hypothesis Testing (T-Test)
# --------------------------------------------------
before = data[data.index < "2020-09-01"]['Close']
after = data[data.index >= "2020-09-01"]['Close']

t, p = stats.ttest_ind(before, after)
print("T-Test:", t)
print("P-Value:", p)

# --------------------------------------------------
# 9. Clustering
# --------------------------------------------------
X = data[['Open', 'Close']]

kmeans = KMeans(n_clusters=3, random_state=0)
data['Cluster'] = kmeans.fit_predict(X)

plt.scatter(data['Open'], data['Close'],
            c=data['Cluster'])
plt.title("K-Means Clustering")
plt.xlabel("Open")
plt.ylabel("Close")
plt.show()
```

### time series analysis - stock market 
```c
import yfinance as yf
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats
from sklearn.cluster import KMeans
from sklearn.linear_model import LinearRegression
from statsmodels.tsa.arima.model import ARIMA

# ----------------------------------
# 1. Load Financial Data
# ----------------------------------
data = yf.download("AAPL", start="2020-01-01", end="2021-01-01")
data = data.dropna()

# ----------------------------------
# 2. Outlier Detection (Z-Score)
# ----------------------------------
z = stats.zscore(data['Close'])
data = data[abs(z) < 3]

# ----------------------------------
# 3. Line Chart
# ----------------------------------
plt.plot(data.index, data['Close'])
plt.title("Apple Stock Prices")
plt.show()

# ----------------------------------
# 4. Histogram
# ----------------------------------
plt.hist(data['Close'], bins=20)
plt.title("Histogram")
plt.show()

# ----------------------------------
# 5. Correlation Heatmap
# ----------------------------------
sns.heatmap(data.corr(), annot=True)
plt.title("Correlation Heatmap")
plt.show()

# ----------------------------------
# 6. Descriptive Statistics
# ----------------------------------
print(data.describe())

# ----------------------------------
# 7. Hypothesis Testing (T-Test)
# ----------------------------------
before = data[data.index < "2020-09-01"]['Close']
after = data[data.index >= "2020-09-01"]['Close']

t, p = stats.ttest_ind(before, after)
print("T-Statistic:", t)
print("P-Value:", p)

# ----------------------------------
# 8. K-Means Clustering
# ----------------------------------
X = data[['Open', 'Close']]

kmeans = KMeans(n_clusters=3, random_state=0, n_init=10)
data['Cluster'] = kmeans.fit_predict(X)

plt.scatter(data['Open'], data['Close'],
            c=data['Cluster'])
plt.xlabel("Open")
plt.ylabel("Close")
plt.title("K-Means Clustering")
plt.show()

# ----------------------------------
# 9. Linear Regression
# ----------------------------------
X = data[['Volume']]
y = data['Close']

model = LinearRegression()
model.fit(X, y)

print("Intercept:", model.intercept_)
print("Coefficient:", model.coef_[0])

# ----------------------------------
# 10. Time Series Forecasting (ARIMA)
# ----------------------------------
ts = data[['Close']].copy()
ts = ts.asfreq('B')
ts['Close'] = ts['Close'].ffill()

arima = ARIMA(ts['Close'], order=(1,0,0))
result = arima.fit()

forecast = result.forecast(5)
print("Forecast:")
print(forecast)
```
### visualization of streaming dataset.
#### weather forecasting
```python
import requests
import matplotlib.pyplot as plt
import time

API_KEY = "YOUR_API_KEY"
CITY = "Hyderabad"

temps = []

for i in range(5):      # collect 5 readings

    url = f"https://api.openweathermap.org/data/2.5/weather?q={CITY}&appid={API_KEY}&units=metric"

    data = requests.get(url).json()

    if "main" in data:
        temps.append(data["main"]["temp"])

    time.sleep(2)

plt.plot(temps, marker='o')
plt.title("Streaming Weather Data")
plt.xlabel("Reading")
plt.ylabel("Temperature")
plt.show()
```
#### stock market code
```python
import yfinance as yf
import matplotlib.pyplot as plt
import time

prices = []

for i in range(5):      # collect 5 readings

    stock = yf.Ticker("AAPL")
    price = stock.history(period="1d")["Close"].iloc[-1]

    prices.append(price)

    time.sleep(2)

plt.plot(prices, marker='o')
plt.title("Streaming Stock Prices")
plt.xlabel("Reading")
plt.ylabel("Price")
plt.show()
```

### market based data analysis and visualization
```python
import yfinance as yf
import matplotlib.pyplot as plt

# ----------------------------------
# 1. Load Market Data
# ----------------------------------
data = yf.Ticker("TCS.NS").history(period="1y")

# ----------------------------------
# 2. Basic Statistics
# ----------------------------------
print(data.describe())
print(data.isnull().sum())

# ----------------------------------
# 3. Daily Returns
# ----------------------------------
data['Daily Return'] = data['Close'].pct_change()

# ----------------------------------
# 4. Closing Price Trend
# ----------------------------------
plt.plot(data['Close'])
plt.title("Closing Price Trend")
plt.show()

# ----------------------------------
# 5. Moving Average
# ----------------------------------
data['MA50'] = data['Close'].rolling(50).mean()

plt.plot(data['Close'], label='Close')
plt.plot(data['MA50'], label='MA50')
plt.legend()
plt.title("Moving Average Analysis")
plt.show()

# ----------------------------------
# 6. Daily Returns Visualization
# ----------------------------------
plt.plot(data['Daily Return'])
plt.title("Daily Returns")
plt.show()

# ----------------------------------
# 7. Histogram of Returns
# ----------------------------------
plt.hist(data['Daily Return'].dropna())
plt.title("Return Distribution")
plt.show()
```

### text visualization using web analytics.
```python
import requests
from bs4 import BeautifulSoup
from collections import Counter
import pandas as pd
import matplotlib.pyplot as plt
from wordcloud import WordCloud
from nltk.corpus import stopwords
import nltk

nltk.download('stopwords')

# Extract text
url = "https://example.com"
html = requests.get(url).text

soup = BeautifulSoup(html, "html.parser")
text = " ".join([p.get_text() for p in soup.find_all('p')])

# Preprocessing
words = text.lower().split()

stop_words = set(stopwords.words('english'))
words = [w for w in words if w.isalnum() and w not in stop_words]

# Frequency Analysis
freq = Counter(words)

df = pd.DataFrame(freq.items(),
                  columns=['Word','Frequency'])

df = df.sort_values(by='Frequency',
                    ascending=False).head(10)

# Bar Chart
plt.bar(df['Word'], df['Frequency'])
plt.title("Top 10 Words")
plt.xticks(rotation=45)
plt.show()

# Word Cloud
wc = WordCloud().generate(text)
plt.imshow(wc)
plt.axis("off")
plt.show()

# Pie Chart
plt.pie(df['Frequency'],
        labels=df['Word'],
        autopct='%1.1f%%')
plt.show()
```

### visualization of various massive datasets - finance, healthcare, census, geospatial.
```python 
import pandas as pd
import matplotlib.pyplot as plt

# Finance Data
plt.plot([2020,2021,2022,2023],
         [100,150,180,250])
plt.title("Finance Data")
plt.show()

# Healthcare Data
plt.bar(['Diabetes','Cancer','Asthma'],
        [200,150,180])
plt.title("Healthcare Data")
plt.show()

# Census Data
plt.pie([500,700,600],
        labels=['0-18','19-35','36-60'],
        autopct='%1.1f%%')
plt.title("Census Data")
plt.show()

# Geospatial Data
plt.scatter([72.87,77.20,77.59],
            [19.07,28.61,12.97])
plt.title("Geospatial Data")
plt.show()
```