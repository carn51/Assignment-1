# Assignment-1
Assignment one data science lab 1 (visualisation)
"""
Created on Wed Feb 19 09:07:02 2025

@author: camil
"""

import numpy as np
import matplotlib.pyplot as plt
import pandas as pd

#import data
df2 = pd.read_csv(r"C:\Users\camil\Downloads\archive (3).zip")
#renaming for clarity/ ease of reference
df2.columns = ['city', 'rank', 'sun_hrs', 'water_cost', 'obesity', 'life_expectancy', 'pollution', 'avg_hrs', 'happiness', 'out_act', 'takeout_number', 'gym_cost']
#print(df2.head())

#first need to find data
years = np.array([2017, 2018, 2019, 2020, 2021, 2022, 2023, 2024])
scores = np.array([6.71, 6.81, 7.05, 7.06, 6.94, 6.8, 6.72, 6.75])
score_malaysia = np.array([6.084, 6.322, 5.339, 5.384, 5.384, 5.711, 6.012, 5.975])

#LINE CHART func, docstring, return 
def linechart(x, y):
    """
    Parameters
    ----------
    x : variable along the x axis, usually Independent
    y : variable along y axis
    Returns
    A very basic line graph
    None.
    """
    plt.plot(x, y)
    plt.title("Function Graph")
    plt.xlabel("IV")
    plt.ylabel("DV")
    plt.show()
    return 
#test 
linechart(years, scores)
#could add legend and color. May use for loops

#func 2 (scatter)
def scatter(x, y, title ="my_title"):
    """
    Parameters
    ----------
    x : value along x axis
    y : value along y axis
    title : TYPE, optional
        DESCRIPTION. The default is "my_title".

    Returns
    -------
    a basic scatter plot
    """
    #try writing my_title in return 
    plt.scatter(x, y)
    plt.xlabel("IV")
    plt.ylabel("DV")
    plt.show()
    return title
#test
scatter(df2['life_expectancy'], df2['happiness'])

#bar function
def barchart(x, height):
    """
    Parameters
    ----------
    x : values along x axis
    height : y axis values or height
    Returns
    a simple bar chart
    None.
    """
    plt.bar(x, height)
    plt.title("Function Bar")
    plt.xlabel("x axis")
    plt.ylabel("y axis")
    plt.show()
    return    
#test
barchart(df2['city'], df2['happiness'])
    
#mean line (for axhlines)
print("Malaysia mean", np.mean(score_malaysia))
print("UK mean", np.mean(scores))

#find standard deviations and use in +-
print("Malaysia std", np.std(score_malaysia))
print("UK std", np.std(scores))

#+- NEEDS SORTING
scores_plus = scores + 0.1335
scores_minus = scores - 0.1335
score_malaysia_plus = score_malaysia + 0.3519
score_malaysia_minus = score_malaysia - 0.3519

#means for scatter plot
ovr_mean_score = np.mean(df2['happiness'])
print(ovr_mean_score)
ovr_mean_le = np.mean(df2['life_expectancy'])
print(ovr_mean_le)

#my plot 1
plt.xlim(2017, 2024)  
plt.ylim(5, 10)
plt.xlabel("Year")
plt.ylabel("Happiness Score")
plt.plot(years, scores, linewidth=2, linestyle="solid", color="blue", label="UK")
plt.plot(years, score_malaysia, linewidth=2, linestyle="solid", color="red",label="Malaysia")
plt.axhline(y=5.776375, color="red", linestyle="dashed")
plt.axhline(y=6.855, color="blue", linestyle="dashed")
plt.legend()
plt.fill_between(scores_plus, scores_minus)
plt.fill_between(score_malaysia_plus, score_malaysia_minus)
plt.show()
#maybe adapt scale, improve

#my scatter plot
plt.scatter(df2['life_expectancy'], df2['happiness'], marker="o")
a, b = np.polyfit(df2["life_expectancy"], df2["happiness"], 1)
plt.plot(df2["life_expectancy"], a*df2["life_expectancy"] + b, color="red", linewidth=1)
plt.axhline(6.435) #MEAN LE AND HAPPINESS
plt.axvline(78.17) #which way round?
plt.title("Happiness and Life Expectancy")
plt.xlabel("Life Expectancy")
plt.ylabel("Happiness Score")

plt.show()

#my bar
plt.bar(df2["city"], df2["happiness"])
plt.title("Happiness Globally")
plt.xlabel("City")
plt.ylabel("Happiness Level")
plt.tick_params(axis='x', pad=5, labelsize=6, labelrotation=90)
plt.axhline(6.435, color="red") 

plt.show()

print(np.corrcoef(df2['life_expectancy'], df2['happiness']))
