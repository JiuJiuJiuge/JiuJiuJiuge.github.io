+++
author = "Yukun Lu"
title = "Change in soil phosphorous distribution and bioavailability within water-stable aggregates under long-term Camellia Oleifera cultivation "
date = "2023-09-25"
description = "Change in soil phosphorous distribution and bioavailability within water-stable aggregates under long-term *Camellia Oleifera* cultivation"
tags = [
    "Submitted in Biology and Fertility of Soils",
]
+++

### **Fig1**
```python
import pandas as pd
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import os
import geopandas as gp
from shapely.geometry import Point
import matplotlib as mpt
mpt.rcParams['font.family'] = "Times New Roman"

data = pd.read_excel("BAF.xlsx")
data

plt.figure(figsize=(4, 4))

#Custom color
dict_color=dict(Chi="#dbe2ef",You="#3f72af",Old="#112d4e")

sns.barplot(x='size',y='BCF1',data=data,hue='age',palette=dict_color,alpha=0.8,capsize=0.1, #Lateral extension width of error line
            saturation=5,errcolor='black',errwidth=0.5,ci=50)#Confidence interval error

#Axis name
plt.xlabel('Soil aggregate size (mm)',fontsize=15)
plt.ylabel('BAF (%)',fontsize=15)

#Range of axes
plt.ylim(0,2000) 

#legend
plt.legend(loc = 'best',frameon=True,fontsize=12,ncol=1)

#Set the scale font size
plt.tick_params(labelsize=15)

plt.savefig(f"Fig/BCF.jpg",bbox_inches="tight",dpi=600)
```
