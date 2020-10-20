```python
import pandas as pd
import seaborn as sns
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
from scipy import stats
```


```python
df = pd.read_csv('epa-sea-level.csv')
    
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>CSIRO Adjusted Sea Level</th>
      <th>Lower Error Bound</th>
      <th>Upper Error Bound</th>
      <th>NOAA Adjusted Sea Level</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1880</td>
      <td>0.000000</td>
      <td>-0.952756</td>
      <td>0.952756</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1881</td>
      <td>0.220472</td>
      <td>-0.732283</td>
      <td>1.173228</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1882</td>
      <td>-0.440945</td>
      <td>-1.346457</td>
      <td>0.464567</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1883</td>
      <td>-0.232283</td>
      <td>-1.129921</td>
      <td>0.665354</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1884</td>
      <td>0.590551</td>
      <td>-0.283465</td>
      <td>1.464567</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>129</th>
      <td>2009</td>
      <td>8.586614</td>
      <td>8.311024</td>
      <td>8.862205</td>
      <td>8.046354</td>
    </tr>
    <tr>
      <th>130</th>
      <td>2010</td>
      <td>8.901575</td>
      <td>8.618110</td>
      <td>9.185039</td>
      <td>8.122973</td>
    </tr>
    <tr>
      <th>131</th>
      <td>2011</td>
      <td>8.964567</td>
      <td>8.661417</td>
      <td>9.267717</td>
      <td>8.053065</td>
    </tr>
    <tr>
      <th>132</th>
      <td>2012</td>
      <td>9.326772</td>
      <td>8.992126</td>
      <td>9.661417</td>
      <td>8.457058</td>
    </tr>
    <tr>
      <th>133</th>
      <td>2013</td>
      <td>8.980315</td>
      <td>8.622047</td>
      <td>9.338583</td>
      <td>8.546648</td>
    </tr>
  </tbody>
</table>
<p>134 rows × 5 columns</p>
</div>




```python
sns.scatterplot(data=df, x="Year", y="CSIRO Adjusted Sea Level")
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1fccbe21108>




![png](output_2_1.png)



```python
x = df['Year']
y = df['CSIRO Adjusted Sea Level']
slope, intercept, r_value, p_value, std_err = stats.linregress(x, y)

list_years_1880_2050 = list(range(1880, 2050)) 
list_1880_2050_intercept = []

for year in list_years_1880_2050:
      list_1880_2050_intercept.append(intercept + slope * year)

sns.scatterplot(data=df, x="Year", y="CSIRO Adjusted Sea Level")
plt.plot(list_years_1880_2050, list_1880_2050_intercept, 'r', label='fitted line')

```




    [<matplotlib.lines.Line2D at 0x1fccbe93408>]




![png](output_3_1.png)



```python
x_2 = df[df['Year'] >= 2000] ['Year']
y_2 = df[df['Year'] >= 2000] ['CSIRO Adjusted Sea Level']

slope_2, intercept_2, r_value_2, p_value_2, std_err_2 = stats.linregress(x_2, y_2)
m = slope_2
b = intercept_2

list_years_2000_2050 = list(range(2000, 2050)) 
list_2000_2050_intercept = []

for year in list_years_2000_2050:
      list_2000_2050_intercept.append(b + m * year)

sns.scatterplot(data=df, x="Year", y="CSIRO Adjusted Sea Level")
plt.plot(list_years_1880_2050, list_1880_2050_intercept, 'r', label='fitted line')
plt.plot(list_years_2000_2050, list_2000_2050_intercept, 'green')
plt.xlabel('Year')
plt.ylabel('Sea Level (inches)')
plt.title('Rise in Sea Level')

```




    Text(0.5, 1.0, 'Rise in Sea Level')




![png](output_4_1.png)



```python

```
