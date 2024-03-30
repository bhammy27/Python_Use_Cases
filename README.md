# Python_Use_Cases
Displaying functions and methods in pandas, matplotlib, seaborn

# Pandas
Dictionaries 
  - list of key value pairs seperated by : and  surround by { }
    - world = {'afghanistan': 30.55, 'albania':2.77}
        - to find population of Albanina
            - print(world['albania'])
  - Add data to dictionary
    - type dictionary name followed by key = value
        - world['sealand'] = 0.000027
  - Delete dictionary value
        - del(world[sealand])
#### import pandas as pd
- stores tabular data in dataframe 
  - brics = ****pd.dataframe(dictionary)****
- set index
    - brics.index = ['BR', 'RU', 'IN', 'CH', 'SA]
    - brics = pd.read_csv('path/to/bics.csv, index_col = 0)
        - index_col = 0 sets index to the value in first row (0)
- Subsetting dictionaries
  - to select all values for country need to use double [[ ]]
      brics[['country]]  or brics[['country,'capital']]
- Slicing rows in pandas
      - .loc or .iloc
        - brics.loc[["RU"]]  still use [[ ]]
  - selecting country, capital and slicing rows
        - brics.loc[['RU','IN','CH'],['country','capital']]
#### Inspecting a DataFame
-  .head() returns first few rows of df
-  .info() shows data type and number of missing values of each columnval
-  .isna() gives true / false values if na
-  .any  adding isna().any() gives boolan of column if any na
-  .shape() returns number of rows and columns in df
-  .describe() calculaes a few summary stats for each column
-  .values() returns Numpy Array of values
-  .columns() index of column names
-  .index() the row index, either row number or names

#### Sorting and Subsetting 
- .sort_values(['col_1','col_2'], ascending = [True,False]) sorts asc then desc
- subset by df['column']
    - dogs[['breed','height_cm']]
    - dogs[dogs['height_cm'] > 50]
    - dogs[dogs['breed'] == 'Labrador']
    - dogs[(dogs['height_cm'] > 50) & (dogs['breed'] == 'Labrador')]
        - or assign varialbes and use:
        - dogs[is_lab & is_tall]
- filter on mutiple values of catagoical data
    - .isin()
    - is_black_or_brown = dogs['color'].isin(['Black','Brown'])
    - dogs[is_black_or_brown]
#### New Columns
- df['new_column'] = values or condition to produce values
- dogs['height_m'] = dogs['height_cm'] / 100
- lets find the tallest dogs with a BMI less than 100
    - bmi_lt_100 = dogs[dogs['bmi'] <100]
    - bmi_lt_100_height = bmi_lt_100.sort_values('height_cm', ascending = False)
    - bmi_lt_100_height[['name','height_cm','bmi']]
 
#### Summary Stats
- .mean() average of values
- .median() middle of all values
- .mode() number appearing most often
- .min() smallest value
      - with dates .min() returns oldest 
- .max() largest value
      - with dates .max() retruns youngest
- .var() how far each number is from the mean
      - measuers spread between numbers in data set
          - larger variance gives more risk or uncertinty
          - smaller variance is less risk or more certin
- .std() square root of variance
          - low std = values closer to mean
          - high std = values farther range from mean
- .quantile()
#### Cumulative Statistics
- .cumsum() cumulative sum of values
- .cummax() max value at that point
- .cummin() min value at that point
- .cumprod() cumulative product

#### Summarizing Catagorical Data
- .drop_duplicates(subset = 'column')
      - if unique values is combination of two columns
      - unique_dogs = vet_visits.drop_duplicates(subset = ['name','breed']
- .value_counts(sort = True, normalize = True)
      - counts catagorical data
      - sort = True puts largest count on top
      - normalize = True turns counts into % total
- .group_by('column')['value'].mean()
      - .agg([min,max, sum]) aggregates values by all statistical measures
      - dogs.group_by(['color','breed'])[['weight','height']].agg([min,max,mean]])
            - selects min max mean height and weight of dogs by color and breed
#### Pivot Tables
- Pivot tables are data frames with sorted indexes
- .pivot_table(values =, index = , columns = ,fill_values = , aggfunc =['np.mean','np.median'], margins = True)
    - values = values wanted in pivot table
    - index = column to set as index
    - columns = 2nd column along top of pivot table
    - fill_values = 0 relpaces all Nan with 0
    - margins = True contains mean of all columns or rows at end
       - allows summary stats of weight, color, and all variables 
    - .agg['np.mean','np.median'] allows aggregation by multiple stats
          - dogs.pivot_table(values = 'weight', index = 'color', columns='breed', fill_vlaue = 0, margins = True)
            - places color as index and breed as columns with mean weight values as values  last row on bottom and right provide summary stats of column or row
#### Indexing
- .set_index('col_name')  sets the column as the index instead of row number
      - can tell column is index because values are left aligned
            - dogs.set_index('name') sets name as index
- .reset_index(drop = True)
      - returns row numbers as index
          - drop = True  removes the index name from pivot table
            - dogs_ind.reset_index(drop = True) removes Name column
- Why use indexing
    - makes subsetting cleaner
        - without name as index
            - dogs[dogs['name'].isin(['Bella','Stella'])
        - with name as index
            - dogs_ind.loc[['Bella','Stella']]
                  - index allows using .loc to subset
    - can have multilevel indexing
        - dogs.set_index(['breed','color])
            - breed is outer level index  color inner level
            - subset on inner level needs use of Tuples
                  - dogs_ind3.loc[[('Labador','Brown'),('Chihuahua','Tan)]]
  - .sort_index(level = ['color','breed'], ascending = [True,False])
  - #### Slicing index
    - OUTER LEVEL indexes
      - dogs.loc['Chow Chow' : 'Poodle']
          - slices all index values from chow to poodle (poodle is included)
    - INNER LEVEL index
      - dogs.loc[("labrador','Brown') : ('Schnauser','Gray')]
  - #### Slicing Columns
    - dogs.loc[:, 'name':'height']
        - sorts all rows (:) and columns name to height
    - dogs.loc[("labrador','Brown') : ('Schnauser','Gray'), 'name':'height']
        - sorts rows brown lab to gray schnauser and columns name to height
          
  
# Matplotlib
#### import matplotlib.pyplot as plt
- plt.plot(x,y) = line chart
- plt.scatter(x,y) = scatter plot
    - s = changes size of marker
    - c = color
    - alpha = transparancy where 1 is non-transparent
- plt.xscale('log') = plots using a logarithmic scale
### Histograms
- plt.hist(variable, n bins,)
### Customization Plots
- plt.xlabel('Year')  names x axis Year
- plt.ylabel('Population')  names y axis Population
- plt.title('World Population Projections') adds this title to chart
- plt.yticks([0,2,4,6,8,10],[0,2B,4B,6B,8B,10B])
    - first list sets y axis scale starting at 0
    - 2nd list adds axis labels so 2 will show 2B
- Annotations
    - plt.text(x,y,'text to insert') inserts text at the x,y coordinates
## Time Series Analysis
- Pandas
  - from datetime import datetime - to manually create dates
  - ****pd.timestamp****(2023-03-15)
      - time will be midnight here 00:00:00
      - timestamp.****year**** returns 2023
      - timestamp.****day_name()**** Returns Wednesday
      - time periods - ****pd.Period("2017-01")***** returns month end
      - period.****asfreq('D')**** returns daily frequency
      - pd.Timestamp('2017-01-31', 'M') +1
          - date with Monthly frequency
          - +1 will return end of month in February 2017
      - Creating Time series
          - ****index = pd.date_range(start, end, periods, freq)****
               - index = pd.date_range(start='2017-01-01, periods=12, freq='M')
               - defult is daily frequency
               - can check using ****pd.DataFrame({'data':index}).info()****
               - Frequencies: H-hour D-day W-week M-Month Q-quater Y-year B-Business days
#### Indexing and Resampling time series
  - convert date string to datetime64
      - ****pd.to_datetime(df['date'])****
    - convert date into index
      - ****df.set_index('date', inplace - True)****
          - Inplace does not create copy
      - ****pd.read_csv('csv', parse_dates=['date'], idnex_col='date')****
  - Can then filter and slice
      - df.['2023'] returns dates for 2023
      - df['2023-3':'2023-6'] slices data in that date range (inclusive of last date)
      - df.loc['2023-3-15', 'price'] returns price on that date
  - Set frequency
      - ****df.asfreq('M')****
      - ****df[df.'price'.isnull()]**** returns missing prices
#### Time Series Calculations
    - df.shoft() moves time series to past or future
        - lead - df.shift() moves shifted date 1 period
        - lag - df.shift(periods = -1) shifts data back 1 period
    - Finincial Return - calculate 1 period percent change
          - df.price.div(df.shifted)
              - divides price by the shifted price column
    - Find relative change in percentage terms
          - df.change.sub(1).mul(100)
                - takes the change column subtracts 1 then gets percentage
          - df.price.diff() difference in value for two periods
          - ****df.column.pct_change(periods=n).mul(100)****
#### Time Series Growth Rates
- Since prices start at different levels normalize price series to start at 100
   - Divide all prices by first in series then multiply by 100
       - Provides same starting point
       - All prices relevent to starting point
       - Difference to starting point is in perentage points
            ****first_price = df.price.iloc[0]
            normalized = df.price.div(first_price).mul(100)
            normalized.plot()****
       - Comparing against a benchmark
           ****index = pd.read_csv('benchmark_csv', parse_dates=['date'], index_col = 'date')
           prices = pd.concat([prices, index], axis=1).dropna()
           normalized = prices.div(prices.iloc[0]).mul(100)
           normalized.plot()
           diff = normalized[tickers].sub(normalized['SP500']),axis = 0)****
#### Changing Frequency    
- DateTImeIndex set using ****.asfreq()**** or ****.reindex()****
- Frequency conversions affect data
    - Upsampling: fill or interpolate missing data
        - Upsampling has higher granularity which shows nulls
        - In example of changing frequency from quarterly to monthly
            ****monthly = monthly.to_frame('baseline')****
              - converts series to DataFrame
            - Fill methods
                ****monthly['ffill'] = quarterly.asfreq('M', method='ffill')****
                ****monthly['bfill'] = quarterly.asfreq('M', method='bfill')****
               ****monthly['value']= quarterly.asfreq('M', fill_value=0)****
    - Downsampling: reduce rows need to aggregate existing data
