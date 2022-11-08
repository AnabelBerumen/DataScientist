## Dataset [NFL](https://www.kaggle.com/datasets/maxhorowitz/nflplaybyplay2009to2016/code)

```python
# get the number of missing data points per column
missing_values_count = nfl_data.isnull().sum()

# look at the # of missing points in the first ten columns
missing_values_count[0:10]
  
  # output
  Date                0
  GameID              0
  Drive               0
  qtr                 0
  down            61154
  time              224
  TimeUnder           0
  TimeSecs          224
  PlayTimeDiff      444
  SideofField       528
  dtype: int64
  ```
  
```python
# how many total missing values do we have?
total_cells = np.product(nfl_data.shape)
total_missing = missing_values_count.sum()

# percent of data that is missing
(total_missing/total_cells) * 100

# output
24.87214126835169
```
```python
# look at the # of missing points in the first ten columns
missing_values_count[0:10]

# output
Date                0
GameID              0
Drive               0
qtr                 0
down            61154
time              224
TimeUnder           0
TimeSecs          224
PlayTimeDiff      444
SideofField       528
dtype: int64
```
```python
# remove all the rows that contain a missing value
nfl_data.dropna()
```
😰😰😰 There is nothing

```python
# remove all columns with at least one missing value
columns_with_na_dropped = nfl_data.dropna(axis=1)
columns_with_na_dropped.head()
```

```python
# get a small subset of the NFL dataset
subset_nfl_data = nfl_data.loc[:, 'EPA':'Season'].head()

# replace all NA's with 0
subset_nfl_data.fillna(0)

# replace all NA's the value that comes directly after it in the same column, 
# then replace all the reamining na's with 0
subset_nfl_data.fillna(method = 'bfill', axis=0).fillna(0)
```
