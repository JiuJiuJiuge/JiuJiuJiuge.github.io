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
## Fig2(c)
```python
# Python
# Import necessary libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Create a figure with a specified size
plt.figure(figsize=(5.5, 3.5))

# Read data from an Excel file named "Data_N2O_LJY_20221021.xlsx" from the 'line' sheet
data = pd.read_excel("Data_N2O_LJY_20221021.xlsx", sheet_name='line')

# Define a dictionary for mapping climate zones to colors
dict_color = dict(Arid="#FB7D07", Semi="#7CFC00", Humid="#0FF1F9", Extreme="#1E90FF")

# Create a bar plot (barplot) with specific settings
ax = sns.barplot(x='climate', y='N2O', data=data, color='dict_color', capsize=0.1,
                 saturation=1, errcolor='k', errwidth=0.5, ci=100)

# Set the y-axis limits and ticks
plt.ylim(0, 400)
plt.yticks([0, 100, 200, 300, 400])

# Set y-axis and x-axis labels
plt.ylabel("$\mathregular{N_2}$O fluxes(μgN·m$^{-2}$·h$^{-1}$)", color='k', fontsize=18)
plt.xlabel('Climate zones', color='k', fontsize=18)

# Set tick label font size and rotate x-axis labels to 0 degrees
plt.tick_params(labelsize=13)
plt.xticks(rotation=0)

# Add text to indicate the subplot as "(c)"
plt.text(-0.4, 360, "(c)", size=20)

# Set the counts for each column
columncounts = [40, 40, 40, 40]

# Define a function to normalize counts to the interval 0-1
def normaliseCounts(widths, maxwidth):
    widths = np.array(widths) / float(maxwidth)
    return widths

# Normalize the counts and adjust the bar widths and positions
widthbars = normaliseCounts(columncounts, 100)
for bar, newwidth in zip(ax.patches, widthbars):
    x = bar.get_x()
    width = bar.get_width()
    centre = x + width / 2.
    bar.set_x(centre - newwidth / 2.)
    bar.set_width(newwidth)

# Save the figure to a file with a specified format, tight layout, and DPI
plt.savefig(f"Fig/Figbar.jpg", bbox_inches="tight", dpi=600)
```
<img src="\images\article3\Fig2.jpg" alt=None/>

## Fig3
```python
# Python
# Arrange the scatter plot in advance
# Import necessary libraries
%matplotlib inline
import pandas as pd
from mpl_toolkits.axisartist.parasite_axes import HostAxes, ParasiteAxes
import matplotlib.pyplot as plt
import matplotlib as mpt
import seaborn as sns
import numpy as np
import matplotlib.ticker as ticker

# Set font family to "Times New Roman"
mpt.rcParams['font.family'] = "Times New Roman"

# Read data from an Excel file named "tree.xlsx"
data = pd.read_excel("tree.xlsx")

# Create a figure with a specified size
plt.figure(figsize=(3.5, 3.5))

# Create a scatter plot with specific settings, including color mapping for 'fluxes' using a Blues colormap
plt.scatter(x='x', y='y', c="fluxes", data=data, cmap='Blues', alpha=1, vmin=0, vmax=200,
            marker='o', s=40, linewidths=0.1, edgecolors='k')

# Add a colorbar with specific settings
cbar = plt.colorbar(orientation='vertical', drawedges=False, shrink=1, pad=0.03)
cbar.ax.set_ylabel('$\mathregular{N_2}$O fluxes(μgN·m$^{-2}$·h$^{-1}$)', size=12)

# Remove y and x-axis labels
plt.ylabel('', fontsize=13)
plt.xlabel('', fontsize=13)

# Set y-axis and x-axis limits
plt.ylim(0, 40)
plt.xlim(0, 7)

# Set tick label font size
plt.tick_params(labelsize=13)

# Save the figure to a file with a specified format, tight layout, and DPI
plt.savefig(f"Fig/Tree.jpg", bbox_inches="tight", dpi=600)
```

<img src="\images\article3\Fig3.jpg" alt=None/>

## Fig4(a)
```python
#python
# Import necessary libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
import os
import geopandas as gp
from shapely.geometry import Point
import seaborn as sns
import matplotlib as mpt
from libtiff import TIFF

# Set the font family to "Times New Roman"
mpt.rcParams['font.family'] = "Times New Roman"

# Read data from an Excel file named "SIZE2.xlsx"
data = pd.read_excel("SIZE2.xlsx")

# Create a figure with a specified size
fig, ax = plt.subplots(figsize=(12, 12))

# Load world map data
world = gp.read_file(gp.datasets.get_path('naturalearth_lowres'))

# Plot the world map as the background
world.plot(ax=ax, color='white', edgecolor='k', linewidth=0.2, alpha=0.8)

# Set the aspect ratio to be equal
ax.set_aspect('equal')

# Create scatter plots for different land cover types with specified colors, sizes, and labels
P1 = plt.scatter(x='Longitude_A', y='Latitude_A', c="#f2a20d", alpha=1, data=data,
                 marker='o', label='Cropland', s="SIZE_A", linewidths=0.1, edgecolors='b')

P2 = plt.scatter(x='Longitude_B', y='Latitude_B', c="#5ca781", alpha=1, data=data,
                 marker='o', label='Forest', s="SIZE_B", linewidths=0.1, edgecolors='b')

P3 = plt.scatter(x='Longitude_C', y='Latitude_C', c="#358b9c", alpha=1, data=data,
                 marker='o', label='Grassland', s="SIZE_C", linewidths=0.1, edgecolors='b')

P4 = plt.scatter(x='Longitude_D', y='Latitude_D', c="#d26763", alpha=1, data=data,
                 marker='o', label='Plantation', s="SIZE_D", linewidths=0.1, edgecolors='b')

# Set y-axis and x-axis limits and tick positions
plt.ylim(-60, 85)
plt.yticks([-50, -25, 0, 25, 50, 75])
plt.xlim(-165, 185)
plt.xticks([-150, -100, -50, 0, 50, 100, 150])

# Set tick label font size
plt.tick_params(labelsize=15)

# Add a text label "(a)"
plt.text(-164, 75, "(a)", size=20)

# Add a legend with specified settings
plt.legend(loc='best', frameon=True, fontsize=15)

# Save the figure to a file with a specified format and DPI
plt.savefig(f"Fig/AI distribution map legend.jpg", bbox_inches="tight", dpi=600)
```

# Fig4(b)
```python
# Python
# Create a new figure with a specified size
plt.figure(figsize=(8, 6))

# Read data from a CSV file, setting 'zone' column as the index
data = pd.read_csv('data.csv', index_col='zone')

# Select specific columns from the data and create a horizontal stacked bar plot
data1 = data[['Cropland', 'Forest', 'Grassland', 'Plantation']]
data1.plot(kind='barh', use_index=True, stacked=True, color=('#f2a20d', '#5ca781', '#358b9c', '#d26763'))

# Set the font size for tick labels
plt.tick_params(labelsize=15)

# Set the label for the x-axis and specify its font size
plt.xlabel('Nitrogen application (KgN·ha$^{-1}$)', fontsize=18)

# Set the x-axis and y-axis limits
plt.xlim(0, 1200)
plt.ylim(-0.8, 3.8)

# Add a legend with specified settings
plt.legend(fontsize=20, ncol=5)

# Add text label "(b)"
plt.text(0, 3.45, "(b)", size=20)

# Save the figure to a file with a specified format and DPI
plt.savefig(f"Fig/fig4(b).jpg", bbox_inches="tight", dpi=600)

```

# Fig4(c)
```python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

def mscatter(x, y, ax=None, m=None, **kw):
    import matplotlib.markers as mmarkers
    if not ax:
        ax = plt.gca()
    sc = ax.scatter(x, y, **kw)
    if (m is not None) and (len(m) == len(x)):
        paths = []
        for marker in m:
            if isinstance(marker, mmarkers.MarkerStyle):
                marker_obj = marker
            else:
                marker_obj = mmarkers.MarkerStyle(marker)
            path = marker_obj.get_path().transformed(marker_obj.get_transform())
            paths.append(path)
        sc.set_paths(paths)
    return sc

N = 15
x = [188.639, 83.606, 252.779, 238.157, 90.2, 324.484, 112.5, 226.117, 56.935, 207.386, 120, 230.513, 89.949, 301.417, 217.477]
y = [112.75, 64.96, 16.94, 110.68, 16.49, 126.5, 18.85, 97.23, 38.59, 69.71, 131.13, 268.38, 43, 137.64, 150.56]
c = [1, 1, 1, 2, 2, 2, 2, 3, 3, 3, 3, 4, 4, 4, 4]
g = [5, 7, 8, 5, 6, 7, 8, 5, 6, 7, 8, 5, 6, 7, 8]
h = {5: '#f2a20d', 6: '#5ca781', 7: '#358b9c', 8: '#d26763'}
m = {1: 'o', 2: 's', 3: 'D', 4: '^'}
cm = list(map(lambda x: m[x], c))
ch = list(map(lambda x: h[x], g))

fig, ax = plt.subplots()

scatter = mscatter(x, y, c=ch, m=cm, ax=ax, cmap=plt.cm.RdYlBu, s=125, edgecolors='black')

# Generate a regression plot using seaborn
data2 = pd.DataFrame({'fertilizer': x, 'fluxes': y})  # Convert x and y to a DataFrame
sns.regplot(x='fertilizer', y='fluxes', data=data2, ci=0, order=1,
            line_kws=dict(color="k", alpha=1, lw=2, zorder=100, linestyle='--'),
            scatter_kws=dict(s=0.00000001, color="k", linewidths=0.04, edgecolors='b', alpha=0.8, zorder=-50))

# Set the axis labels
plt.xlabel('Nitrogen application (KgN·ha$^{-1}$)', fontsize=18)
plt.ylabel('$\mathregular{N_2}$O fluxes (μgN·m$^{-2}$·h$^{-1}$)', fontsize=18)

# Adjust the font size of ticks
plt.tick_params(labelsize=15)

# Save the figure
plt.savefig("Fig/point.jpg", bbox_inches="tight", dpi=600)

# Display the plot (optional)
plt.show()
```

<img src="\images\article3\Fig4.jpg" alt=None/>