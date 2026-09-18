# ECE-2112-PA-4

**Made by: Sophia Marielle R. Quizon | 2ECE-B**

The content of this repository contains the Programming Assignment for the course Advanced Computer Programming and Algorithms for the S.Y. 2026-2027.

## A. VISAYAS COMMUNICATION DATAFRAME

The Visayas Communication DataFrame problem loads tha `board.csv` dataset into Pandas DataFrame named `df`. The Average of each student is first calculated from the Math, Electronics, GEAS, and Communication scores. The program uses Boolean conditions to select students whose Hometown is Visayas and whose Track is Communication. From these students, only the required columns Name, Gender, Math, Electronics, and Average are selected.

The following methods are used: 

• ` df['Average'] = df[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)` - Calculates the Average of the four subject scores for each student.

• `df.loc []`- Select rows and columns based on the given conditions and column labels.

• `(df ['Hometown'] == 'Visayas') & (df ['Track'] == 'Communication')` - Identifies students whose Hometown is Visayas and whose Track is Communication.

The combination of the different operations gives the final function:

```python
import pandas as pd

df = pd.read_csv ('/board2.csv')
df

Average = df['Average'] = df[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)
Average

df = df.assign (Average=Average)
df

VisComm = df.loc [(df ['Hometown'] == 'Visayas') & (df ['Track'] == 'Communication'), ['Name', 'Gender', 'Math', 'Electronics', 'Average']]
VisComm
```

The Boolean conditions allow the students to be filtered according to both their Hometown and Track before the required columns are selected. The resulting DataFrame contains the students who satisfy both conditions.

## B. VISAYAS FEMALE DATAFRAME

The Visayas Female DataFrame problem uses Boolean indexing to locate students whose Hometown is Visayas and whose Gender is Female. The result is stored in VisFemale, while the columns should be Name, Track, GEAS,, Electronics, and Average are retained. A second df names VisFemale_60 is then created to display only the students whose Average is at least 60.

The following methods are used: 

• `df.loc []` - Select rows and columns based on the given conditions and column labels.

• `(df ['Hometown'] == 'Visayas') & (df ['Gender'] == 'Female')` - Identifies students whose Hometown is Visayas and the Gender is Female.

• `VisFemale.loc [VisFemale ['Average'] >= 60]` - Identifies students whose Average is at least 60.

The combination of the different operations gives the final function:

```python
VisFemale = df.loc [(df ['Hometown'] == 'Visayas') & (df ['Gender'] == 'Female'), ['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
VisFemale

VisFemale_60 = VisFemale.loc [VisFemale ['Average'] >= 60] 
VisFemale_60
```

## C. CATEGORY-AVERAGE VISUALIZATION

The category-average visualization problem examines how the recorded Average differs across the categorical features Track, Gender, and Hometown. The program first calculates the mean of Average for every category using Pandas. Three summary DataFrames are then created to display the calculated means. Lastly, one figure containing three 
bar charts is created to compare the mean of Average by Track, Gender, and Hometown.

The following methods are used: 


• `df.loc []` - Select rows and columns based on the given conditions and column labels.

• `.mean()` - Calculates the mean Average of each category.

• `pd.DataFrame()` - Creates summary DataFrames containing the categories and their corresponding mean Average.

• `plt.subplots()` - Creates one figure containing three separate bar charts.

• `.set_title()` - Adds a title to each graph.

• `.set_xlabel()` and `set_ylabel` - Adds labels to the x and y axis.

The combination of the different operations gives the final function:

```python

# Tracks
Communication = df.loc [df ['Track'] == 'Communication', 'Average'].mean()
Instrumentation = df.loc [df ['Track'] == 'Instrumentation', 'Average'].mean()
Microelectronics = df.loc [df ['Track'] == 'Microelectronics', 'Average'].mean()

print ('Communication Average:', Communication)
print ('Instrumental Average:', Instrumentation)
print ('Microelectronics Average:', Microelectronics)

# Gender

Female = df.loc [df ['Gender'] == 'Female', 'Average'].mean()
Male = df.loc [df ['Gender'] == 'Male', 'Average'].mean()

print ('Female Average:', Female)
print ('Male Average:', Male)

#Hometown

Luzon = df.loc [df ['Hometown'] == 'Luzon', 'Average'].mean()
Visayas = df.loc [df ['Hometown'] == 'Visayas', 'Average'].mean()
Mindanao = df.loc [df ['Hometown'] == 'Mindanao', 'Average'].mean()

print ('Luzon Average:', Luzon)
print ('Visayas Average:', Visayas)
print ('Mindanao Average:', Mindanao)

---

# Track Mean Average

TrackMeanAverage = {
    'Track': ['Communication', 'Instrumentation', 'Microelectronics'],
    'Average': [Communication, Instrumentation, Microelectronics],

}
TrackMeanAverage = pd.DataFrame(TrackMeanAverage)
TrackMeanAverage

# Gender Mean Average

GenderMeanAverage = {
    'Gender': ['Female', 'Male'],
    'Average': [Female, Male],

}
GenderMeanAverage = pd.DataFrame(GenderMeanAverage)
GenderMeanAverage

# Hommetown Mean Average

HometownMeanAverage = {
    'Gender': ['Luzon', 'Visayas', 'Mindanao'],
    'Average': [Luzon, Visayas, Mindanao],

}
HometownMeanAverage = pd.DataFrame(HometownMeanAverage)
HometownMeanAverage

```

The three summary DataFrames are used to create one figure containing bar charts:

```python
import matplotlib.pyplot as plt
fig, axes = plt.subplots (1, 3, figsize=(15, 5))

TrackMeanAverage.plot(x='Track', y='Average', kind = 'bar', ax = axes[0])
axes[0].set_title ('Mean Average by Track')
axes[0].set_ylabel ('Mean Average')
axes[0].set_xlabel ('Track')
axes[0].tick_params (axis='x', rotation=45)

GenderMeanAverage.plot(x='Gender', y='Average', kind = 'bar', ax = axes[1])
axes[1].set_title ('Gender Average by Track')
axes[1].set_ylabel ('Mean Average')
axes[1].set_xlabel ('Gender')
axes[1].tick_params (axis='x', rotation=0)

HometownMeanAverage.plot(x='Gender', y='Average', kind = 'bar', ax = axes[2])
axes[2].set_title ('Hometown Average by Track')
axes[2].set_ylabel ('Mean Average')
axes[2].set_xlabel ('Hometown')
axes[2].tick_params (axis='x', rotation=45)

plt.tight_layout ()
plt.show ()
```

The calculated sample means are then compares using `.max()` to identify the category with the highest observed mean for each feature.

```python

Highest_TrackMean = TrackMeanAverage.loc [TrackMeanAverage ['Average'] == TrackMeanAverage['Average'].max()]
Highest_GenderMean = GenderMeanAverage.loc [GenderMeanAverage ['Average'] == GenderMeanAverage ['Average'].max()]
Highest_HometownMean = HometownMeanAverage.loc [HometownMeanAverage ['Average'] == HometownMeanAverage ['Average'].max()]

print (f"{Highest_TrackMean['Track'].iloc[0]} had the highest mean Average among the Track categories.")
print (f"{Highest_GenderMean['Gender'].iloc[0]} had the highest sample mean Average among the Gender categories.")
print (f"{Highest_HometownMean['Gender'].iloc[0]} had the highest sample mean Average among the Hometown categories.")

df.groupby('Track')['Average'].mean()
df.groupby('Gender')['Average'].mean()
df.groupby('Hometown')['Average'].mean()
```

The observed results show that Communication has the highest sample mean among the Track categories, Male has the highest sample mean among the Gender categories, and Luzon has the highest among the Hometown categories. These results describe the observed dataset only and do not establish that a category causes a higher board-exam score.

Thank you for reading!

For reference of the main python program for Programming Assignment 1, kindly click the link and download: https://github.com/sphmrlle/ECE-2112-PA-4

README file Version History:
September 16, 2026 - Initial README ouput uploaded and drafted.

September 17, 2026 - Final README updated
