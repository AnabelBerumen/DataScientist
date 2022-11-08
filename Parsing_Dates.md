[Python strftime cheatsheet](https://strftime.org/)

Some examples:

> 1/17/07 has the format "%m/%d/%y"

> 17-1-2007 has the format "%d-%m-%Y"


```python
# create a new column, date_parsed, with the parsed dates
landslides['date_parsed'] = pd.to_datetime(landslides['date'], format="%m/%d/%y")
```
```python
# print the first few rows
landslides['date_parsed'].head()

# output
0   2007-03-02
1   2007-03-22
2   2007-04-06
3   2007-04-14
4   2007-04-15
Name: date_parsed, dtype: datetime64[ns]
```

#### What if I run into an error with multiple date formats? While we're specifying the date format here, sometimes you'll run into an error when there are multiple date formats in a single column. If that happens, you can have pandas try to infer what the right date format should be. You can do that like so:
```python
landslides['date_parsed'] = pd.to_datetime(landslides['Date'], infer_datetime_format=True)
```
#### Why don't you always use infer_datetime_format = True? There are two big reason
```python
earthquakes.loc[3378, "Date"] = "02/23/1975"
earthquakes.loc[7512, "Date"] = "04/28/1985"
earthquakes.loc[20650, "Date"] = "03/13/2011"
earthquakes['date_parsed'] = pd.to_datetime(earthquakes['Date'], format="%m/%d/%Y")"""s not to always have pandas guess the time format. The first is that pandas won't always been able to figure out the correct date format, especially if someone has gotten creative with data entry. The second is that it's much slower than specifying the exact format of the dates.
```
```python
# get the day of the month from the date_parsed column
day_of_month_landslides = landslides['date_parsed'].dt.day
day_of_month_landslides.head()

# output
0     2.0
1    22.0
2     6.0
3    14.0
4    15.0
Name: date_parsed, dtype: float64
```
```python
# remove na's
day_of_month_landslides = day_of_month_landslides.dropna()

# plot the day of the month
sns.distplot(day_of_month_landslides, kde=False, bins=31)
```
```python
# Exercise
# Convert our date columns to datetime
earthquakes[3378:3383]
>>> 3378	1975-02-23T02:58:41.000Z
# We can get an idea of how widespread this issue is by checking the length of each entry in the "Date" column

date_lengths = earthquakes.Date.str.len()
date_lengths.value_counts()

>>> 10    23409
>>> 24        3
>>> ame: Date, dtype: int64

indices = np.where([date_lengths == 24])[1]
print('Indices with corrupted data:', indices)
earthquakes.loc[indices]

>>> Indices with corrupted data: [ 3378  7512 20650]
earthquakes.iloc[3378,0] = "02/23/1975"
earthquakes.iloc[7512,0] = "04/28/1985"
earthquakes.iloc[20650,0]= "03/13/2011"

earthquakes['date_parsed'] = pd.to_datetime(earthquakes['Date'], format='%m/%d/%Y')
# %m	09	Month as a zero-padded decimal number.
# %d	08	Day of the month as a zero-padded decimal number.
# %Y	2013	Year with century as a decimal number.
```

```python
# my baby n.n
date_lengths = volcanos['Last Known Eruption'].str.len()
date_lengths.value_counts()

>>>
7    1312
8     129
6      62
5       3
9       1
4       1

indices = np.where([date_lengths == 7])[1]
print('Indices with corrupted data:', indices)
volcanos.loc[indices]

# CD and AD common era
import re
for indice in date_lengths:
    if re.findall('BCE', volcanos.loc[indice, 'Last Known Eruption']):
   
        volcanos.loc[indice, 'Last Known Eruption'] = volcanos.loc[indice, 'Last Known Eruption'].replace('BCE', 'BC')
    elif re.findall('CE', volcanos.loc[indice, 'Last Known Eruption']):
        
        volcanos.loc[indice, 'Last Known Eruption'] = volcanos.loc[indice, 'Last Known Eruption'].replace('CE',' ')
    elif re.findall('AD', volcanos.loc[indice, 'Last Known Eruption']):
        
        volcanos.loc[indice, 'Last Known Eruption'] = volcanos.loc[indice, 'Last Known Eruption'].replace('AD',' ')
    
    
 ```

