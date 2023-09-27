+++
author = "Yukun Lu"
title = "Global nitrous oxide flux emissions in different climate zones "
date = "2023-09-25"
description = "Global nitrous oxide flux emissions in different climate zones"
tags = [
    "Writing",
]
+++

## Fig1(a)
```python
#Python
#fig map
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
import calendar

# Read data
data = pd.read_excel("Sites distribution map.xlsx")

# Set the font family for matplotlib
mpt.rcParams['font.family'] = "Times New Roman"

# Create a figure and axis with a specified size
fig, ax = plt.subplots(figsize=(12, 12))

# Load world map data from geopandas
world = gp.read_file(gp.datasets.get_path('naturalearth_lowres'))

# Plot the world map with specific styling
world.plot(ax=ax, color='white', edgecolor='k', linewidth=0.2, alpha=0.8)

# Set the aspect ratio to equal for a more accurate representation
ax.set_aspect('equal')

# Create scatter plots for different data points (P1, P2, P3, P4) with specific colors, labels, and markers
P1 = plt.scatter(x='Longitude_A', y='Latitude_A', c="#FB7D07", alpha=1, data=data, marker='o', label='Arid', s=45, linewidths=0.2, edgecolors='b')
P2 = plt.scatter(x='Longitude_B', y='Latitude_B', c="#7CFC00", alpha=1, data=data, marker='o', label='Semi arid and humid', s=45, linewidths=0.2, edgecolors='b')
P3 = plt.scatter(x='Longitude_C', y='Latitude_C', c="#0FF1F9", alpha=1, data=data, marker='o', label='Humid', s=45, linewidths=0.2, edgecolors='b')
P4 = plt.scatter(x='Longitude_D', y='Latitude_D', c="#1E90FF", alpha=1, data=data, marker='o', label='Extreme humid', s=45, linewidths=0.2, edgecolors='b')

# Set y-axis and x-axis limits and ticks
plt.ylim(-60, 85)
plt.yticks([-50, -25, 0, 25, 50, 75])
plt.xlim(-165, 185)
plt.xticks([-150, -100, -50, 0, 50, 100, 150])

# Set tick label font size
plt.tick_params(labelsize=13)

# Add text to indicate the subplot as "(a)"
plt.text(-160, 75, "(a)", size=20)

# Add a legend with specified location, frame, and font size
plt.legend(bbox_to_anchor=(0.001, 0.01), loc='lower left', frameon=True, fontsize=13)

# Save the figure to a file with a specified format, tight layout, and DPI
plt.savefig(f"Fig/sites distribution map legend.jpg", bbox_inches="tight", dpi=600)
```
## Fig1(b)
```python
#Python
# Define the x-axis labels and corresponding values
x = ["Arid", "Semi arid and humid", "Humid", "Extreme Humid"]
y = (66, 99, 96, 181)

# Create a bar plot with specified x-axis labels and colors
plt.bar(x, y, width=0.4, color=("#FB7D07", "#7CFC00", "#0FF1F9", "#1E90FF"))

# Set tick label font size
plt.tick_params(labelsize=15)

# Set x and y axis labels
plt.xlabel('Climate zones', fontsize=17)
plt.ylabel('Number of sites', fontsize=17)

# Save the figure to a file with a specified format, tight layout, and DPI
plt.savefig(f"Fig/Fig_bar.jpg", bbox_inches="tight", dpi=600)
```
## Fig1(c)
```python
# Python
# Arid
# Create a figure with a specified size
plt.figure(figsize=(2.5, 2.5))

# Define the data values and labels for the pie chart
data = [170, 8, 68, 24, 3]
labels = ["Cropland", "Forest", "Grassland", "Plantation", "Other"]

# Create a pie chart with custom settings
plt.pie(data, pctdistance=0.75, autopct='%.1f%%', colors=["#ca6924", "#0c8918", "#66C3B1", "#e29c45", "#EBE8BF"])

# Create a white circle at the center to make it look like a donut chart
plt.pie([1], radius=0.5, colors='w')

# Set the title for the pie chart
plt.title('Arid', fontsize=17)

# Save the figure to a file with a specified format, tight layout, and DPI
plt.savefig(f"Fig/Fig_pie_arid.jpg", bbox_inches="tight", dpi=600)
```
<img src="\images\article3\Fig1.jpg" alt=None/>

## Fig2(a)
```python
# Python
# We pre-graded the nitrous oxide emissions and set the appropriate size
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

# Read data from an Excel file named "N2O.xlsx"
data = pd.read_excel("N2O.xlsx")

# Create a figure and axis with a specified size
fig, ax = plt.subplots(figsize=(12, 12))

# Load world map data from geopandas
world = gp.read_file(gp.datasets.get_path('naturalearth_lowres'))

# Plot the world map with specific styling
world.plot(ax=ax, color='white', edgecolor='k', linewidth=0.2, alpha=0.8)

# Set the aspect ratio to equal for a more accurate representation
ax.set_aspect('equal')

# Create scatter plots for different data points (P1, P2, P3, P4) with specific colors, labels, and markers
P1 = plt.scatter(x='Longitude_A', y='Latitude_A', c="#FB7D07", alpha=1, data=data, marker='o', label='Arid', s=data["SIZE_A"], linewidths=0.2, edgecolors='b')
P2 = plt.scatter(x='Longitude_B', y='Latitude_B', c="#7CFC00", alpha=1, data=data, marker='o', label='Semi arid and humid', s=data["SIZE_B"], linewidths=0.2, edgecolors='b')
P3 = plt.scatter(x='Longitude_C', y='Latitude_C', c="#0FF1F9", alpha=1, data=data, marker='o', label='Humid', s=data["SIZE_C"], linewidths=0.2, edgecolors='b')
P4 = plt.scatter(x='Longitude_D', y='Latitude_D', c="#1E90FF", alpha=1, data=data, marker='o', label='Extreme humid', s=data["SIZE_D"], linewidths=0.2, edgecolors='b')

# Set y-axis and x-axis limits and ticks
plt.ylim(-60, 85)
plt.yticks([-50, -25, 0, 25, 50, 75])
plt.xlim(-165, 185)
plt.xticks([-150, -100, -50, 0, 50, 100, 150])

# Set tick label font size
plt.tick_params(labelsize=15)

# Add text to indicate the subplot as "(a)"
plt.text(-160, 75, "(a)", size=20)

# Add a legend with specified location, frame, and font size
plt.legend(loc='best', frameon=True, fontsize=15)

# Save the figure to a file with a specified format, tight layout, and DPI
plt.savefig(f"Fig/AI distribution map legend.jpg", bbox_inches="tight", dpi=600)
```

## Fig2(b)
```python
# Python
# Import necessary libraries
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

# Read data from an Excel file named "Data_N2O_LJY_20221021.xlsx"
data = pd.read_excel("Data_N2O_LJY_20221021.xlsx", sheet_name='line')

# Create a figure with a specified size
plt.figure(figsize=(5.5, 3.5))

# Create a regression plot (regplot) with specific settings
sns.regplot(x='latitude', y='N2O', data=data, ci=30, order=3,
            line_kws=dict(color="k", alpha=1, lw=2, zorder=100, linestyle='--'),
            scatter_kws=dict(s=0.00000001, color="k", linewidths=0.04, edgecolors='b', alpha=0.8, zorder=-50))

# Create a scatter plot with color mapping for 'P/PET' using a rainbow colormap
plt.scatter(x="latitude", y="N2O", data=data, c="P/PET", cmap='rainbow_r', alpha=1, linewidths=0.2, edgecolors='black', vmin=0.2, vmax=1.8, s=30)

# Add a colorbar with specific settings
cbar = plt.colorbar(orientation='vertical', drawedges=False, shrink=1, pad=0.03)
cbar.ax.set_ylabel('AI', size=18)

# Set x and y axis labels
plt.xlabel('Latitudes(°)', fontsize=18)
plt.ylabel('$\mathregular{N_2}$O fluxes(μgN·m$^{-2}$·h$^{-1}$)', fontsize=18)

# Set y-axis limits
plt.ylim(-500, 1500)

# Set tick label font size
plt.tick_params(labelsize=15)
cbar.ax.tick_params(labelsize=12)

# Add text to indicate the subplot as "(b)"
plt.text(-5, 1300, "(b)", size=20)

# Save the figure to a file with a specified format, tight layout, and DPI
plt.savefig(f"Fig/FigN2O_flux_SW_PPET.jpg", bbox_inches="tight", dpi=600)
```
