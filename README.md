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

    
