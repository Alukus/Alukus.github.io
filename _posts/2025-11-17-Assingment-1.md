---
title: 'Assingment 1'
date: 2025-11-17
permalink: /posts/2025/11/Assingment-1/
tags:
  - Assingment
---
<details>
<summary>Click to show code</summary>
  
```py
import pandas as pd
import matplotlib.pyplot as plt
from scipy.stats import pearsonr

my_dataset = pd.read_excel('Graph_Plot.xlsx', sheet_name=0)
my_dataset.columns = my_dataset.columns.str.strip()

# element columns
As = my_dataset["As"]
Sb = my_dataset["Sb"]
Fe = my_dataset["Fe"]
Zn = my_dataset["Zn"]
Cu = my_dataset["Cu"]
Ag = my_dataset["Ag"]

fig = plt.figure(figsize=(10, 8))

# ------------------------- Plot 1 -------------------------
ax1 = fig.add_subplot(2, 2, 1)
ax1.scatter(As, Sb, marker='x', label="cross")
r1, p1 = pearsonr(As, Sb)
ax1.text(0.05, 0.95, f"r = {r1:.2f}", transform=ax1.transAxes,
         ha='left', va='top', fontsize=10)
ax1.set_xlabel("As [apfu]")
ax1.set_ylabel("Sb [apfu]")
ax1.set_xlim([0, 4])
ax1.set_ylim([0, 4])

# ------------------------- Plot 2 -------------------------
ax2 = fig.add_subplot(2, 2, 2)
ax2.scatter(Fe, Zn, marker='o', label="circle")
r2, p2 = pearsonr(Fe, Zn)
ax2.text(0.05, 0.95, f"r = {r2:.2f}", transform=ax2.transAxes,
         ha='left', va='top', fontsize=10)
ax2.set_xlabel("Fe [apfu]")
ax2.set_ylabel("Zn [apfu]")
ax2.set_xlim([0, 2])
ax2.set_ylim([0, 2])

# ------------------------- Plot 3 -------------------------
ax3 = fig.add_subplot(2, 2, 3)
ax3.scatter(Cu, Ag, marker='^', label="triangle")
r3, p3 = pearsonr(Cu, Ag)
ax3.text(0.05, 0.95, f"r = {r3:.2f}", transform=ax3.transAxes,
         ha='left', va='top', fontsize=10)
ax3.set_xlabel("Cu [apfu]")
ax3.set_ylabel("Ag [apfu]")

# ------------------------- Plot 4 -------------------------
x_ratio = Sb / (Sb + As)
y_ratio = Fe / (Fe + Zn)

Ten_Fe = (x_ratio < 0.5) & (y_ratio >= 0.25)
Ten_Zn = (x_ratio < 0.5) & (y_ratio < 0.25)
Tet_Fe = (x_ratio >= 0.5) & (y_ratio >= 0.25)
Tet_Zn = (x_ratio >= 0.5) & (y_ratio < 0.25)

ax4 = fig.add_subplot(2, 2, 4)

# markers
ax4.scatter(x_ratio[Ten_Fe], y_ratio[Ten_Fe],
            edgecolors='red', facecolors='none', marker='o',
            label="Ten-(Fe)")

ax4.scatter(x_ratio[Ten_Zn], y_ratio[Ten_Zn],
            edgecolors='lime', facecolors='none', marker='s',
            label="Ten-(Zn)")

ax4.scatter(x_ratio[Tet_Fe], y_ratio[Tet_Fe],
            edgecolors='red', facecolors='none', marker='o',
            label="Tet-(Fe)")

ax4.scatter(x_ratio[Tet_Zn], y_ratio[Tet_Zn],
            edgecolors='lime', facecolors='none', marker='s',
            label="Tet-(Zn)")

#boundary lines
ax4.axvline(0.5, color='gray', linewidth=0.5)
ax4.axhline(0.25, color='gray', linewidth=0.5)

# labels
ax4.set_xlabel("Sb / (Sb + As) [apfu]")
ax4.set_ylabel("Fe / (Fe + Zn) [apfu]")

# domain text
ax4.text(0.25, min(y_ratio)*1.05, "Ten-(Zn)", fontsize=10,
         ha='center', va='center')
ax4.text(0.75, min(y_ratio)*1.05, "Tet-(Zn)", fontsize=10,
         ha='center', va='center')

ax4.text(0.25, max(y_ratio)*0.95, "Ten-(Fe)", 
         fontsize=10, ha='center', va='center')
ax4.text(0.75, max(y_ratio)*0.95, "Tet-(Fe)", 
         fontsize=10, ha='center', va='center')



# plot limits
ax4.set_ylim([0, 0.5])
ax4.set_xlim([0, 1])
ax4.legend()

# -------------------------
fig.tight_layout()
plt.show()
```
</details>
  
This script loads a geochemical dataset from Excel and produces a four-panel figure where the first three plots show elemental relationships (As–Sb, Fe–Zn, Cu–Ag) with Pearson correlation coefficients added directly on each subplot, while the fourth plot converts Sb–As and Fe–Zn data into apfu ratios to classify samples into Ten-(Fe), Ten-(Zn), Tet-(Fe), and Tet-(Zn).

<img src="/images/Assignment_1.png" width="800">
