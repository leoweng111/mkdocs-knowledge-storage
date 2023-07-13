# United States - Crime Rates - 1960 - 2014

Check out [Crime Rates Exercises Video Tutorial](https://youtu.be/46lmk1JvcWA) to watch a data scientist go through the exercises

### Introduction:

This time you will create a data 

Special thanks to: https://github.com/justmarkham for sharing the dataset and materials.

### Step 1. Import the necessary libraries


```python
import numpy as np
import pandas as pd
```

### Step 2. Import the dataset from this [address](https://raw.githubusercontent.com/guipsamora/pandas_exercises/master/04_Apply/US_Crime_Rates/US_Crime_Rates_1960_2014.csv). 

### Step 3. Assign it to a variable called crime.


```python
url = "https://raw.githubusercontent.com/guipsamora/pandas_exercises/master/04_Apply/US_Crime_Rates/US_Crime_Rates_1960_2014.csv"
crime = pd.read_csv(url)
crime.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>Population</th>
      <th>Total</th>
      <th>Violent</th>
      <th>Property</th>
      <th>Murder</th>
      <th>Forcible_Rape</th>
      <th>Robbery</th>
      <th>Aggravated_assault</th>
      <th>Burglary</th>
      <th>Larceny_Theft</th>
      <th>Vehicle_Theft</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1960</td>
      <td>179323175</td>
      <td>3384200</td>
      <td>288460</td>
      <td>3095700</td>
      <td>9110</td>
      <td>17190</td>
      <td>107840</td>
      <td>154320</td>
      <td>912100</td>
      <td>1855400</td>
      <td>328200</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1961</td>
      <td>182992000</td>
      <td>3488000</td>
      <td>289390</td>
      <td>3198600</td>
      <td>8740</td>
      <td>17220</td>
      <td>106670</td>
      <td>156760</td>
      <td>949600</td>
      <td>1913000</td>
      <td>336000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1962</td>
      <td>185771000</td>
      <td>3752200</td>
      <td>301510</td>
      <td>3450700</td>
      <td>8530</td>
      <td>17550</td>
      <td>110860</td>
      <td>164570</td>
      <td>994300</td>
      <td>2089600</td>
      <td>366800</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1963</td>
      <td>188483000</td>
      <td>4109500</td>
      <td>316970</td>
      <td>3792500</td>
      <td>8640</td>
      <td>17650</td>
      <td>116470</td>
      <td>174210</td>
      <td>1086400</td>
      <td>2297800</td>
      <td>408300</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1964</td>
      <td>191141000</td>
      <td>4564600</td>
      <td>364220</td>
      <td>4200400</td>
      <td>9360</td>
      <td>21420</td>
      <td>130390</td>
      <td>203050</td>
      <td>1213200</td>
      <td>2514400</td>
      <td>472800</td>
    </tr>
  </tbody>
</table>
</div>



### Step 4. What is the type of the columns?


```python
crime.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 55 entries, 0 to 54
    Data columns (total 12 columns):
    Year                  55 non-null int64
    Population            55 non-null int64
    Total                 55 non-null int64
    Violent               55 non-null int64
    Property              55 non-null int64
    Murder                55 non-null int64
    Forcible_Rape         55 non-null int64
    Robbery               55 non-null int64
    Aggravated_assault    55 non-null int64
    Burglary              55 non-null int64
    Larceny_Theft         55 non-null int64
    Vehicle_Theft         55 non-null int64
    dtypes: int64(12)
    memory usage: 5.2 KB


##### Have you noticed that the type of Year is int64. But pandas has a different type to work with Time Series. Let's see it now.

### Step 5. Convert the type of the column Year to datetime64


```python
# pd.to_datetime(crime)
crime.Year = pd.to_datetime(crime.Year, format='%Y')
crime.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 55 entries, 0 to 54
    Data columns (total 12 columns):
    Year                  55 non-null datetime64[ns]
    Population            55 non-null int64
    Total                 55 non-null int64
    Violent               55 non-null int64
    Property              55 non-null int64
    Murder                55 non-null int64
    Forcible_Rape         55 non-null int64
    Robbery               55 non-null int64
    Aggravated_assault    55 non-null int64
    Burglary              55 non-null int64
    Larceny_Theft         55 non-null int64
    Vehicle_Theft         55 non-null int64
    dtypes: datetime64[ns](1), int64(11)
    memory usage: 5.2 KB


### Step 6. Set the Year column as the index of the dataframe


```python
crime = crime.set_index('Year', drop = True)
crime.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Population</th>
      <th>Total</th>
      <th>Violent</th>
      <th>Property</th>
      <th>Murder</th>
      <th>Forcible_Rape</th>
      <th>Robbery</th>
      <th>Aggravated_assault</th>
      <th>Burglary</th>
      <th>Larceny_Theft</th>
      <th>Vehicle_Theft</th>
    </tr>
    <tr>
      <th>Year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1960-01-01</th>
      <td>179323175</td>
      <td>3384200</td>
      <td>288460</td>
      <td>3095700</td>
      <td>9110</td>
      <td>17190</td>
      <td>107840</td>
      <td>154320</td>
      <td>912100</td>
      <td>1855400</td>
      <td>328200</td>
    </tr>
    <tr>
      <th>1961-01-01</th>
      <td>182992000</td>
      <td>3488000</td>
      <td>289390</td>
      <td>3198600</td>
      <td>8740</td>
      <td>17220</td>
      <td>106670</td>
      <td>156760</td>
      <td>949600</td>
      <td>1913000</td>
      <td>336000</td>
    </tr>
    <tr>
      <th>1962-01-01</th>
      <td>185771000</td>
      <td>3752200</td>
      <td>301510</td>
      <td>3450700</td>
      <td>8530</td>
      <td>17550</td>
      <td>110860</td>
      <td>164570</td>
      <td>994300</td>
      <td>2089600</td>
      <td>366800</td>
    </tr>
    <tr>
      <th>1963-01-01</th>
      <td>188483000</td>
      <td>4109500</td>
      <td>316970</td>
      <td>3792500</td>
      <td>8640</td>
      <td>17650</td>
      <td>116470</td>
      <td>174210</td>
      <td>1086400</td>
      <td>2297800</td>
      <td>408300</td>
    </tr>
    <tr>
      <th>1964-01-01</th>
      <td>191141000</td>
      <td>4564600</td>
      <td>364220</td>
      <td>4200400</td>
      <td>9360</td>
      <td>21420</td>
      <td>130390</td>
      <td>203050</td>
      <td>1213200</td>
      <td>2514400</td>
      <td>472800</td>
    </tr>
  </tbody>
</table>
</div>



### Step 7. Delete the Total column


```python
del crime['Total']
crime.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Population</th>
      <th>Violent</th>
      <th>Property</th>
      <th>Murder</th>
      <th>Forcible_Rape</th>
      <th>Robbery</th>
      <th>Aggravated_assault</th>
      <th>Burglary</th>
      <th>Larceny_Theft</th>
      <th>Vehicle_Theft</th>
    </tr>
    <tr>
      <th>Year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1960-01-01</th>
      <td>179323175</td>
      <td>288460</td>
      <td>3095700</td>
      <td>9110</td>
      <td>17190</td>
      <td>107840</td>
      <td>154320</td>
      <td>912100</td>
      <td>1855400</td>
      <td>328200</td>
    </tr>
    <tr>
      <th>1961-01-01</th>
      <td>182992000</td>
      <td>289390</td>
      <td>3198600</td>
      <td>8740</td>
      <td>17220</td>
      <td>106670</td>
      <td>156760</td>
      <td>949600</td>
      <td>1913000</td>
      <td>336000</td>
    </tr>
    <tr>
      <th>1962-01-01</th>
      <td>185771000</td>
      <td>301510</td>
      <td>3450700</td>
      <td>8530</td>
      <td>17550</td>
      <td>110860</td>
      <td>164570</td>
      <td>994300</td>
      <td>2089600</td>
      <td>366800</td>
    </tr>
    <tr>
      <th>1963-01-01</th>
      <td>188483000</td>
      <td>316970</td>
      <td>3792500</td>
      <td>8640</td>
      <td>17650</td>
      <td>116470</td>
      <td>174210</td>
      <td>1086400</td>
      <td>2297800</td>
      <td>408300</td>
    </tr>
    <tr>
      <th>1964-01-01</th>
      <td>191141000</td>
      <td>364220</td>
      <td>4200400</td>
      <td>9360</td>
      <td>21420</td>
      <td>130390</td>
      <td>203050</td>
      <td>1213200</td>
      <td>2514400</td>
      <td>472800</td>
    </tr>
  </tbody>
</table>
</div>



### Step 8. Group the year by decades and sum the values

#### Pay attention to the Population column number, summing this column is a mistake


```python
# To learn more about .resample (https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.resample.html)
# To learn more about Offset Aliases (http://pandas.pydata.org/pandas-docs/stable/timeseries.html#offset-aliases)

# Uses resample to sum each decade
crimes = crime.resample('10AS').sum()

# Uses resample to get the max value only for the "Population" column
population = crime['Population'].resample('10AS').max()

# Updating the "Population" column
crimes['Population'] = population

crimes
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Population</th>
      <th>Violent</th>
      <th>Property</th>
      <th>Murder</th>
      <th>Forcible_Rape</th>
      <th>Robbery</th>
      <th>Aggravated_assault</th>
      <th>Burglary</th>
      <th>Larceny_Theft</th>
      <th>Vehicle_Theft</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1960</th>
      <td>201385000</td>
      <td>4134930</td>
      <td>45160900</td>
      <td>106180</td>
      <td>236720</td>
      <td>1633510</td>
      <td>2158520</td>
      <td>13321100</td>
      <td>26547700</td>
      <td>5292100</td>
    </tr>
    <tr>
      <th>1970</th>
      <td>220099000</td>
      <td>9607930</td>
      <td>91383800</td>
      <td>192230</td>
      <td>554570</td>
      <td>4159020</td>
      <td>4702120</td>
      <td>28486000</td>
      <td>53157800</td>
      <td>9739900</td>
    </tr>
    <tr>
      <th>1980</th>
      <td>248239000</td>
      <td>14074328</td>
      <td>117048900</td>
      <td>206439</td>
      <td>865639</td>
      <td>5383109</td>
      <td>7619130</td>
      <td>33073494</td>
      <td>72040253</td>
      <td>11935411</td>
    </tr>
    <tr>
      <th>1990</th>
      <td>272690813</td>
      <td>17527048</td>
      <td>119053499</td>
      <td>211664</td>
      <td>998827</td>
      <td>5748930</td>
      <td>10568963</td>
      <td>26750015</td>
      <td>77679366</td>
      <td>14624418</td>
    </tr>
    <tr>
      <th>2000</th>
      <td>307006550</td>
      <td>13968056</td>
      <td>100944369</td>
      <td>163068</td>
      <td>922499</td>
      <td>4230366</td>
      <td>8652124</td>
      <td>21565176</td>
      <td>67970291</td>
      <td>11412834</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>318857056</td>
      <td>6072017</td>
      <td>44095950</td>
      <td>72867</td>
      <td>421059</td>
      <td>1749809</td>
      <td>3764142</td>
      <td>10125170</td>
      <td>30401698</td>
      <td>3569080</td>
    </tr>
  </tbody>
</table>
</div>



### Step 9. What is the most dangerous decade to live in the US?


```python
# apparently the 90s was a pretty dangerous time in the US
crime.idxmax(0)
```




    Population            2010
    Violent               1990
    Property              1990
    Murder                1990
    Forcible_Rape         1990
    Robbery               1990
    Aggravated_assault    1990
    Burglary              1980
    Larceny_Theft         1990
    Vehicle_Theft         1990
    dtype: int64


