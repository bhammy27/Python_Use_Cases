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
    - 

    
