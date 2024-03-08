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
-  .info() shows data type and number of missing values of each column
-  .shape() returns number of rows and columns in df
-  .describe() calculaes a few summary stats for each column
-  .values() returns Numpy Array of values
-  columns() index of column names
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
- .max() largest value
- .var() how far each number is from the mean
      - measuers spread between numbers in data set
          - larger variance gives more risk or uncertinty
          - smaller variance is less risk or more certin
- .std() square root of variance
          - low std = values closer to mean
          - high std = values farther range from mean


  
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

    
