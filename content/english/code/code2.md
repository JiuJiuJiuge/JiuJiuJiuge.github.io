+++
author = "Yukun Lu"
title = "Change in soil phosphorous distribution and bioavailability within water-stable aggregates under long-term Camellia Oleifera cultivation "
date = "2023-09-25"
description = "Change in soil phosphorous distribution and bioavailability within water-stable aggregates under long-term *Camellia Oleifera* cultivation"
tags = [
    "Submitted in Biology and Fertility of Soils",
]
+++

## **Fig1**
```python
#Python
#Fig1(b)
# Import necessary libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import os
import geopandas as gp
from shapely.geometry import Point
import matplotlib as mpt

# Set the font family for matplotlib
mpt.rcParams['font.family'] = "Times New Roman"

# Read data from an Excel file named "BAF.xlsx"
data = pd.read_excel("BAF.xlsx")

# Create a bar plot figure with a specified size
plt.figure(figsize=(4, 4))

# Define a color dictionary for age groups
dict_color = dict(Chi="#dbe2ef", You="#3f72af", Old="#112d4e")

# Create a bar plot using Seaborn
sns.barplot(x='size', y='BAF', data=data, hue='age', palette=dict_color, alpha=0.8, capsize=0.1,
            saturation=5, errcolor='black', errwidth=0.5, ci=50)

# Set x and y axis labels
plt.xlabel('Soil aggregate size (mm)', fontsize=15)
plt.ylabel('BAF (%)', fontsize=15)

# Set the y-axis limits
plt.ylim(0, 2000)

# Add a legend with specified location, frame, and font size
plt.legend(loc='best', frameon=True, fontsize=12, ncol=1)

# Set tick label font size
plt.tick_params(labelsize=15)

# Save the figure to a file with a specified format, tight layout, and DPI
plt.savefig(f"Fig/BCF.jpg", bbox_inches="tight", dpi=600)

#Same with Fig1(a)
```

## Fig2  
```python
#Python
#Fig2(a) LM
# Import necessary libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import os
import geopandas as gp
from shapely geometry import Point
import matplotlib as mpt

# Set the font family for matplotlib
mpt.rcParams['font.family'] = "Times New Roman"

# Read data from an Excel file named "Pcontent.xlsx"
data = pd.read_excel("Pcontent.xlsx")

# Create a bar plot figure with a specified size
plt.figure(figsize=(5, 4))

# Define a color dictionary for age groups
dict_color = dict(Chi="#caddd1", You="#719f85", Old="#4a565f")

# Create a bar plot using Seaborn
sns.barplot(x='P', y='concentration', data=data, hue='age', palette=dict_color, alpha=0.8, capsize=0.1,
            saturation=5, errcolor='black', errwidth=0.5, ci=95)

# Set x and y axis labels
plt.xlabel('', fontsize=15)
plt.ylabel('Concentrations of soil-P fraction (mg·kg$^{-1}$)', fontsize=14)

# Set the y-axis limits
plt.ylim(0, 50)

# Set x-axis tick labels
plt.gca().set_xticklabels(['Al-P', 'Fe-P', 'O-P', 'Ca-P'])

# Add a legend with specified location, frame, and font size
plt.legend(loc='best', frameon=True, fontsize=12)

# Set tick label font size
plt.tick_params(labelsize=17)

# Save the figure to a file with a specified format, tight layout, and DPI
plt.savefig(f"Fig/LM.jpg", bbox_inches="tight", dpi=600)

#Same with others
```

## Fig3
```python
#Python
#Fig3(a)
# Import necessary libraries
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.metrics import r2_score

# Read data from an Excel file
data = pd.read_excel("absorb.xlsx",sheet_name='LM')

# Define a Langmuir adsorption model function
def langmuir(x, a, b):
    return a * x * b / (1 + b * x)

# Define a dictionary for custom colors based on age groups
dict_color = dict(Chi="#ff5959", You="#ffad5a", Old="#4f9da6")

# Create a Seaborn FacetGrid for plotting
g = sns.FacetGrid(data, hue='age', palette=dict_color, height=6)

# Plot scatter points on the FacetGrid
g.map(sns.scatterplot, 'P', 'absorb', s=60, linewidth=0.2, edgecolors="black", alpha=0.8, zorder=-30)

# Generate x values for the Langmuir model curve
x = np.linspace(0, 7, 100)
line_width = 5
line_alpha = 0.7

# Iterate through unique age groups in the data
for i, age_group in enumerate(data['age'].unique()):
    age_data = data[data['age'] == age_group]
    
    # Perform curve fitting using the Langmuir model
    popt, pcov = curve_fit(langmuir, age_data['P'], age_data['absorb'], p0=[3, 1])
    y_fit = langmuir(x, *popt)
    
    # Calculate and print the R-squared value for the fit
    r2 = r2_score(age_data['absorb'], langmuir(age_data['P'], *popt))
    print(f"{age_group} curve fit: a={popt[0]:.2f}, b={popt[1]:.2f}, R^2={r2:.2f}")
    
    # Plot the fitted curve for the age group
    plt.plot(x, y_fit, color=dict_color[age_group], lw=line_width, alpha=line_alpha, label=f'{age_group}')

# Set y-axis limits and ticks
plt.ylim(-100, 1900)
plt.yticks([0, 400, 800, 1200, 1600, 2000])

# Set x-axis ticks
plt.xticks([0, 1, 2, 3, 4, 5, 6, 7])

# Set x and y-axis labels and tick label sizes
plt.xlabel('Equilibrium concentration (mg·L$^{-1}$)', fontsize=25)
plt.ylabel('Adsorption quantity (mg·kg$^{-1}$)', fontsize=25)
plt.tick_params(labelsize=22)

# Remove unnecessary plot borders
sns.despine(top=False, right=False, left=False, bottom=False)

# Save the figure to a file
plt.savefig(f"Fig/LM.jpg", bbox_inches="tight", dpi=600)
# Same as others
```

## Fig4(a)
```python
# Python


```