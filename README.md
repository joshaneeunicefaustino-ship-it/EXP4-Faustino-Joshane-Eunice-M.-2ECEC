# EXPERIMENT 4: DATA WRANGLING AND DATA VISUALIZATION
> **Name:** *Joshane Eunice M. Faustino*
> 
> **Section:** *2ECE-C*
> 
> **Date:** *September 17, 2026*

> # I. Intended Learning Outcomes
At the end of this laboratory activity, the student should be able to:
1. filter tabular data using several categorical and numerical conditions;
2. construct focused DataFrames by selecting relevant features;
3. summarize the relationship between categorical features and a numerical variable; and
4. communicate a data comparison using clear and correctly labeled plots.

> # What is pandas?
- short for **Python Data Analysis**
- it is a core Python library that provides high-performance,
easy-to-use data structures and data analysis tools
for the Python programming language.
- this is used for this programming assignment

> # What is Data wrangling?

- Data wrangling (also called data munching)
involves manipulation and transformation
of data frames in preparation for data
analytics and/or machine learning
application.
q The main objective of data wrangling is to
make data useful.

> # MATPLOTLIB
-  In Python, data visualization is done by using the
MATPLOTLIB package.
- Matplotlib is a comprehensive library for creating static,
animated, and interactive visualizations in Python.

# III. Programming Problems

> Use the same ECE Board Exam 2 dataset supplied for Experiment 4. Work in a Jupyter Notebook
using Pandas and a Python plotting library used in class. Use the dataset’s existing column labels,
including Name, Gender, Track, Hometown, Math, GEAS, Electronics, and Average.

**- Pandas as pd was imported in order to access the library pandas and to also shorten pandas  
instead of typing it multiple times ```import pandas as pd```**

- ```import``` is used to bring a Python library into the program, while ```as pd``` gives pandas a shorter name that can be used when calling its functions.

**-matplotlib.pyplot was imported in order to access the library and to also shorten into plt  
instead of typing matplotlib.pyplot multiple times```import matplotlib.pyplot as plt ```**

- ```pyplot``` is a module used for creating plots and graphs, while ```as plt``` gives it a shorter name for easier use in the code.

**CODE:** ```df = pd.read_excel("board2.xlsx")```

The ```pd.read_excel()``` function in Pandas is used to read data from Excel files into a Pandas DataFrame. It is assigned as df.

- ```read_excel()``` is a Pandas function used to read data from an Excel file and store it as a DataFrame.

**CODE:**  ```data = df.copy()```
- The .copy() method in Python is used to create a shallow copy of a list or dictionary. This means that it creates a new object, but does not create copies of nested objects within the original object.
- ```.copy()``` creates a separate copy of the DataFrame so that changes made to ```data``` will not directly modify the original ```df```.

**CODE:**  ```data["Average"] = data[["Math", "GEAS", "Electronics", "Communication"]].mean(axis=1)```
- This code is used include a column average of those included in [] which is ["Math", "GEAS", "Electronics", "Communication"]

- ```data[[...]]``` selects the columns Math, GEAS, Electronics, and Communication.
- ```.mean(axis=1)``` calculates the mean across each row, so each student gets one Average based on the four subject scores.
- ```axis=1``` means the calculation is performed horizontally across the columns.
- 
# A. VISAYAS COMMUNICATION DATAFRAME

> Create a DataFrame named VisComm containing students whose Hometown is Visayas and whose Track
is Communication. Retain only these columns, in the stated order:

**CODE:** 
```
VisComm = data[
    (data["Hometown"] == "Visayas") &
    (data["Track"] == "Communication")
][["Name", "Gender", "Math", "Electronics", "Average"]]
```
- The code used boolean conditioning in which it only showed columns Name, Gender, Math, Electronics, and Average
- It also has a condition that under the column Hometown, only Visayas should be shown and under Track only Communications.
  
> Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to
the source dataset before the columns are selected.

**CODE:**
```Number_Rows = len(VisComm)```
- len(df) shows the # of rows in DataFrame.
  
# B. VISAYAS FEMALE DATAFRAME

> Create a second DataFrame named VisFemale containing students whose Hometown is Visayas and
whose Gender is Female. Retain only:

 **CODE:**
```
VisFemale = data[
    (data["Hometown"] == "Visayas") &
    (data["Gender"] == "Female")
][["Name", "Track", "GEAS", "Electronics", "Average"]]
```
- The code used boolean conditioning in which it only showed columns Name, Track, GEAS, Electronics, and Average
- It also has a condition that under the column Hometown, only Visayas should be shown and under Gender only Female.
- So the template is like (dataframe[selected column] == "find word")
  - ```==``` checks whether the value matches the specified category.
- ```&``` means both conditions must be true.

> Display VisFemale. Then display only the rows of VisFemale whose Average is at least 60. Do not
overwrite VisFemale when performing this second filter.

**CODE:**
```VisFemale.loc[VisFemale["Average"] >= 60]```
- it used ```.loc``` to locate the Average of the given data frame earlier.
- it also used boolean, greater than or equal to sign
  
# C. CATEGORY-AVERAGE VISUALIZATION

> a. For each feature, compute the mean of Average for every category using Pandas.
**CODE:**
```
track_mean = data.groupby("Track", as_index=False)["Average"].mean()

print("Mean Average by Track:")
track_mean
```
- This code used group data specifically groupby.
- The template is like df.groupby(<what group> ="") Return a GroupBy object, grouped by values in column named "col".
- It used ```mean()``` to compute for the mean
- The ```print()``` was used to show a specific text
- This all goes to the rest of the gender_mean and hometown_mean
**CODE:**
```
gender_mean = data.groupby("Gender", as_index=False)["Average"].mean()

print("Mean Average by Gender:")
gender_mean
```
**CODE:**
```
hometown_mean = data.groupby("Hometown", as_index=False)["Average"].mean()

print("Mean Average by Hometown:")
hometown_mean
```
> b. Display the three summary tables.
- We can yung the function ```display(dataframe)``` to show the the tables called out, but in jupyter notebook we can just drop what we named it.
  
> c. Create one figure containing three bar charts: mean Average by Track, by Gender, and by
Hometown.

**CODE:**
```
df["Average"] = df[["Math", "GEAS", "Electronics", "Communication"]].mean(axis=1)

track_mean = df.groupby("Track")["Average"].mean()
gender_mean = df.groupby("Gender")["Average"].mean()
hometown_mean = df.groupby("Hometown")["Average"].mean()

plt.figure()
track_mean.plot(kind="bar", color="purple")
plt.title("Mean Average by Track")
plt.ylabel("Average")
plt.show()

plt.figure()
gender_mean.plot(kind="bar", color="pink")
plt.title("Mean Average by Gender")
plt.ylabel("Average")
plt.show()

plt.figure()
hometown_mean.plot(kind="bar", color="blue")
plt.title("Mean Average by Hometown")
plt.ylabel("Average")
plt.show()
```
- In this code we used functions like:
- ```plt.figure()``` creates a new figure for the plot.
- ```.plot(kind="bar")``` creates a bar chart from the grouped mean values.
- ```plt.title()``` adds a title to the chart.
- ```plt.ylabel()``` labels the y-axis.
- ```plt.show()``` displays the figure in the notebook.
- The three separate ```plt.figure()``` commands create three individual bar charts.
- ```kind="bar"``` specifies that a bar chart will be used.

> d. Below the figure, write three concise statements identifying the category with the highest sample
mean for each feature

1. As we look at the track, **Communications students*** showed the highest sample mean average.
2. As I compare the genders which is Male and Female as stated, ***Male students*** recorded the highest sample mean average.
3. Across hometown regions, ***Luzon students*** showed the highest sample mean average.

>Interpretation rule: Describe the observed dataset only. A difference in group means does not, by
itself, establish that a feature causes a higher board-exam score.

### Interpretation
These results only describe patterns within this specific sample. A higher group mean doesn't prove that Track, Gender, or Hometown causes better board-exam performance — other underlying factors could be responsible, and the group sizes here are fairly small to draw strong conclusions from.

