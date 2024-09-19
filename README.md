#  Experiment 4 

# I. Intended Learning Outcomes:
  1. Identify the codes and functions needed in cleaning and visualizing data.
  2. Be able to apply and use the different codes and functions in creating a Python program that will be used in data wrangling and data visualization

# II. Instructions:
 Download the ECE Board Exam 2 dataset found on this link: ECE Board Exam Dataset and write a Python script/code in the Jupyter Notebook to do the given problems. You may submit your Jupyter notebook in the dedicated submission bin .

 ## Problem 1
### Instructions:
Create the following data frames based on the format provided:
Example: Vis = [“Name”, “Gender”, “Track”, “Math<70”]; hometown is constant as Visayas

a. Filename: Instru = [“Name”, “GEAS”, “Electronics >70”]; where track is constant as
Instrumentation and hometown Luzon

b. Filename: Mindy = [ “Name”, “Track”, “Electronics”, “Average >=55”]; where hometown is
constant as Mindanao and gender Female

```python

# A. 
import pandas as pd #To access pandas library

#Open the file
#Make sure that you also download the file in the same folder where your notebook is

df = pd.read_excel('board2.xlsx')
df

#Create DataFrame 'Instru'
instru = df.loc[
    (df['Electronics'] > 70) & (df['Hometown'] == 'Luzon') & (df['Track'] == 'Instrumentation'),
    ['Name', 'GEAS', 'Electronics']
]
instru

#B.
#Calculate the average
if 'Average' not in df.columns:
    df['Average'] = df[['Math', 'Electronics', 'GEAS']].mean(axis=1)

# Create DataFrame 'Mindy' 
mindy = df.loc[
    (df['Average'] >= 55) & (df['Hometown'] == 'Mindanao') & (df['Gender'] == 'Female'),
    ['Name', 'Track', 'Electronics', 'Average']
]
mindy  # Display the DataFrame

```
 ## Problem 2
 
 ### Instructions:
 Create a visualization that shows how the different features contributes to average grade. Does
chosen track in college, gender, or hometown contributes to a higher average score?

```python

import matplotlib.pyplot as plt
import seaborn as sns
#Calculate the average score across Math, Electronics, and GEAS for each student
df['Average'] = df[['Math', 'Electronics', 'GEAS']].mean(axis=1)

#Function to plot scores by Track and Hometown, separated by Gender
def plot_scores(df, columns, hue='Gender'):
    for col in columns:
        # Plot by Track
        sns.barplot(x='Track', y=col, hue=hue, data=df, palette='viridis')
        plt.title(f'{col} Scores by Track and {hue}')
        plt.xlabel('Track')
        plt.ylabel(f'{col} Score')
        plt.show()

        # Plot by Hometown
        sns.barplot(x='Hometown', y=col, hue=hue, data=df, palette='magma')
        plt.title(f'{col} Scores by Hometown and {hue}')
        plt.xlabel('Hometown')
        plt.ylabel(f'{col} Score')
        plt.show()
#Generate the graph for Math, Electronics, GEAS, and Average scores
plot_scores(df, ['Math', 'Electronics', 'GEAS', 'Average'])

