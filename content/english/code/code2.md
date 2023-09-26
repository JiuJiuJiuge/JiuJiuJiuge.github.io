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

sns.barplot(x='size',y='BAF',data=data,hue='age',palette=dict_color,alpha=0.8,capsize=0.1, #Lateral extension width of error line
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
#Same with Fig1(a)
```

## Fig2  
```python
#Python
#Fig2(a) LM
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

data = pd.read_excel("Pcontent.xlsx")
data

plt.figure(figsize=(5, 4))

#Custom color
dict_color=dict(Chi="#caddd1",You="#719f85",Old="#4a565f")

sns.barplot(x='P',y='concentration',data=data,hue='age',palette=dict_color,alpha=0.8,capsize=0.1, #Lateral extension width of error line
            saturation=5,errcolor='black',errwidth=0.5,ci=95)#Confidence interval error

#Axis name
plt.xlabel('',fontsize=15)
plt.ylabel('Concentrations of soil-P fraction(mg·kg$^{-1}$)',fontsize=14)

#Range of axis
plt.ylim(0,50) 

plt.gca().set_xticklabels(['Al-P', 'Fe-P', 'O-P', 'Ca-P'])

#legend
plt.legend(loc = 'best',frameon=True,fontsize=12)

#Scale font size
plt.tick_params(labelsize=17)


plt.savefig(f"Fig/LM.jpg",bbox_inches="tight",dpi=600)
#Same with others
```

## Fig3
```python

```