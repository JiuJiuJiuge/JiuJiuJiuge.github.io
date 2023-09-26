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
# Import necessary libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import os
import geopandas as gp
from shapely.geometry import Point
from matplotlib.colors import ListedColormap 
import seaborn as sns
import matplotlib as mpt
from libtiff import TIFF

# Set the font family for matplotlib
mpt.rcParams['font.family'] = "Times New Roman"

# Read data from an Excel file named "adata.xlsx" from different sheets
data2 = pd.read_excel("adata.xlsx", sheet_name='Mi')
data1 = pd.read_excel("adata.xlsx", sheet_name='SM')
data = pd.read_excel("adata.xlsx", sheet_name='LM')

# Create a figure with a specified size
plt.figure(figsize=(5, 4))

# Create a regression plot with confidence interval and scatter plot for data2
sns.regplot(x='SOM', y='AlP', data=data2, ci=95, order=1,
            line_kws=dict(color="#ec748b", alpha=1, lw=2, zorder=100, linestyle='-'),
            scatter_kws=dict(s=0.00000001, color="k", linewidths=0.04, edgecolors='b', alpha=0.8, zorder=-50))

# Create a scatter plot for data2
plt.scatter(x="SOM", y="AlP", data=data2, color="#ec748b", alpha=1, linewidths=0.2, edgecolors='black', vmin=0.2, vmax=1.8)

# Create a regression plot with confidence interval and scatter plot for data1
sns.regplot(x='SOM', y='AlP', data=data1, ci=95, order=1,
            line_kws=dict(color="#6eb1de", alpha=1, lw=2, zorder=100, linestyle='-'),
            scatter_kws=dict(s=0.00000001, color="k", linewidths=0.04, edgecolors='b', alpha=0.8, zorder=-50))

# Create a scatter plot for data1
plt.scatter(x="SOM", y="AlP", data=data1, alpha=1, color="#6eb1de", linewidths=0.2, edgecolors='black', vmin=0.2, vmax=1.8)

# Create a regression plot with confidence interval and scatter plot for data
sns.regplot(x='SOM', y='AlP', data=data, ci=95, order=1,
            line_kws=dict(color="#6bb952", alpha=1, lw=2, zorder=100, linestyle='-'),
            scatter_kws=dict(s=0.00000001, color="k", linewidths=0.04, edgecolors='b', alpha=0.8, zorder=-50))

# Create a scatter plot for data
plt.scatter(x="SOM", y="AlP", data=data, color="#6bb952", alpha=1, linewidths=0.2, edgecolors='black', vmin=0.2, vmax=1.8, s=40)

# Set y-axis and x-axis labels
plt.ylabel('Al-P (mg·kg$^{-1}$)', fontsize=22)
plt.xlabel('SOM (g·kg$^{-1}$)', fontsize=22)
 
# Set y-axis limits and ticks
plt.ylim(-15, 30)
plt.yticks([-15, 0, 15, 30]) 

# Set tick label font size
plt.tick_params(labelsize=18)

# Add a legend with specified location, frame, font size, and other properties
plt.legend(loc="right", frameon=False, fontsize=12, markerscale=1, bbox_to_anchor=(2, 0.0))

# Save the figure to a file with a specified format, tight layout, and DPI
plt.savefig(f"Fig/alp_som.jpg", bbox_inches="tight", dpi=600)
# Same as others
```

## Fig4(b)
```python
# The slope and significance were calculated using SPSS in advance
# Import necessary libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import os
import geopandas as gp
from shapely.geometry import Point
from matplotlib.colors import ListedColormap 
import seaborn as sns
import matplotlib as mpt
from libtiff import TIFF

# Create a bar plot figure with a specified size
plt.figure(figsize=(5, 4))

# Define the x-axis values and the corresponding slopes
index = np.arange(5)
values = [0.22, 0, 0.09, 0, -0.41]

# Create a bar plot with specified colors
plt.bar(index, values, color=["#6bb952", 'b', "#6eb1de", 'b', "#ec748b"], alpha=1)

# Set y-axis and x-axis limits and ticks
plt.ylim(-0.5, 0.5) 
plt.xlim(-1, 5)
plt.xticks([0, 1, 2, 3, 4, 5]) 

# Set x-axis tick labels
plt.gca().set_xticklabels(['> 2', "", '2-0.25', "", '< 0.25'])

# Set x and y axis labels
plt.xlabel('Soil aggregate size (mm)', fontsize=22)
plt.ylabel('Slope', fontsize=22)

# Set tick label font size
plt.tick_params(labelsize=18)

# Add a horizontal line at y=0 for reference
plt.axhline(0, color='black', linestyle=":", alpha=0.5)

# Save the figure to a file with a specified format, tight layout, and DPI
plt.savefig(f"Fig/alp_slope.jpg", bbox_inches="tight", dpi=600)
# Same as ohters
```

## Fig5(a)
```python
#Python
#Fig5(a)
# Import necessary libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import os
import geopandas as gp
from shapely.geometry import Point
import seaborn as sns
import matplotlib as mpt
from libtiff import TIFF

# Set the font family for matplotlib
mpt.rcParams['font.family'] = "Times New Roman"

# Read data from an Excel file named "adata.xlsx" from the 'line' sheet
data = pd.read_excel("adata.xlsx", sheet_name='line')

# Create a figure with a specified size
plt.figure(figsize=(4, 4))

# Create a regression plot with confidence interval and scatter plot for 'AlP' vs. 'C=C'
sns.regplot(y='C=C', x='AlP', data=data, ci=95, order=1,
            line_kws=dict(color="#3951A2", alpha=1, lw=2, zorder=100, linestyle='-'),
            scatter_kws=dict(s=0.00000001, color="k", linewidths=0.04, edgecolors='b', alpha=0.8, zorder=-50))

# Create a scatter plot for 'AlP' vs. 'C=C'
plt.scatter(y="C=C", x="AlP", data=data, color="#3951A2", alpha=1, linewidths=0.2, edgecolors="black", vmin=0.2, vmax=1.8)

# Create regression plots and scatter plots for other variables ('FeP', 'OP', 'CaP')
sns.regplot(y='C=C', x='FeP', data=data, ci=95, order=1,
            line_kws=dict(color="#72AACF", alpha=1, lw=2, zorder=100, linestyle='-'),
            scatter_kws=dict(s=0.00000001, color="k", linewidths=0.04, edgecolors='b', alpha=0.8, zorder=-50))
plt.scatter(y="C=C", x="FeP", data=data, alpha=1, color="#72AACF", linewidths=0.2, edgecolors='black', vmin=0.2, vmax=1.8)

sns.regplot(y='C=C', x='OP', data=data, ci=95, order=1,
            line_kws=dict(color="#FDB96B", alpha=1, lw=2, zorder=100, linestyle='-'),
            scatter_kws=dict(s=0.00000001, color="k", linewidths=0.04, edgecolors='b', alpha=0.8, zorder=-50))
plt.scatter(y="C=C", x="OP", data=data, color="#FDB96B", alpha=1, linewidths=0.2, edgecolors='black', vmin=0.2, vmax=1.8, s=40)

sns.regplot(y='C=C', x='CaP', data=data, ci=95, order=1,
            line_kws=dict(color="#EC5D3B", alpha=1, lw=2, zorder=100, linestyle='-'),
            scatter_kws=dict(s=0.00000001, color="k", linewidths=0.04, edgecolors='b', alpha=0.8, zorder=-50))
plt.scatter(y="C=C", x="CaP", data=data, color="#EC5D3B", alpha=1, linewidths=0.2, edgecolors='black', vmin=0.2, vmax=1.8, s=40)

# Set x and y axis labels
plt.xlabel('Content (mg·kg$^{-1}$)', fontsize=22)
plt.ylabel('C=C (%)', fontsize=22)

# Set x and y axis limits and ticks
plt.xlim(-10, 60)
plt.ylim(-40, 80)
plt.yticks([-40, -20, 0, 20, 40, 60, 80])

# Set tick label font size
plt.tick_params(labelsize=18)

# Save the figure to a file with a specified format, tight layout, and DPI
plt.savefig(f"Fig/total_C=C.jpg", bbox_inches="tight", dpi=600)
#Same as Fig5(b)
```

## Fig5(c)
```python
#Calculate the slope and significance using SPSS in advance
# Import necessary libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import os
import geopandas as gp
from shapely.geometry import Point
import seaborn as sns
import matplotlib as mpt
from libtiff import TIFF

# Create a bar plot figure with a specified size
plt.figure(figsize=(4, 4))

# Define the x-axis values and the corresponding slopes
index = np.arange(4)
values = [-0.898, -0.641, -1.489, -0.352]

# Create a bar plot with specified colors
plt.bar(index, values, color=["#3951A2", '#72AACF', "#FDB96B", "#EC5D3B"], alpha=1)

# Set y-axis and x-axis limits and ticks
plt.ylim(-2, 2)
plt.yticks([-2, -1, 0, 1, 2])
plt.xlim(-0.8, 3.8)
plt.xticks([0, 1, 2, 3])

# Set x-axis tick labels
plt.gca().set_xticklabels(['Al-P', "Fe-P", 'O-P', "Ca-P"])

# Set x and y axis labels
plt.xlabel('', fontsize=22)
plt.ylabel('Slope', fontsize=22)

# Set tick label font size
plt.tick_params(labelsize=18)

# Add a horizontal line at y=0 for reference
plt.axhline(0, color='black', linestyle=":", alpha=0.5)

# Save the figure to a file with a specified format, tight layout, and DPI
plt.savefig(f"Fig/totalC=C_slope.jpg", bbox_inches="tight", dpi=600)
# Same as Fig5(d)
```

Fig6