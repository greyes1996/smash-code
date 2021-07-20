# Final Project Information!
This is code provided for my students in the 2021 SMASH Academy!

On this page, you can find details regarding the final project code I wrote as a sample final project assignment (thanks to Brendan Smith who also used GitHub for a similar purpose!

# My Question
I wanted to know the difference between Hipsanic Males and Females between who passed the AP Calculus exams.


# My code
Below is a copy of my code for this project. Let's start with our data and how I selected the rows and columns that I needed.

First, always remember to import the Pandas library and set it as pd (or a variable of your choosing!). And then don't forget to upload the data that you'll need!
```python:
import pandas as pd

# This line will read in the dataset
# Be sure to update this to the correct name of your dataset!
data = pd.read_csv("CSY1Data.csv", thousands=",")
```
Next, we'll need to select only the columns that are relevant to my question. Since I am only asking about Hispanic/Latino students, I need to select those columns. Below is the code I used for that. 

Note: if you are also planning to select multiple columns, you can copy and paste this code and replace the "data" variable with the name of your variable and then replace the text in "" with the name of the columns you want to get. 
```python:
hisp_data = data[["AP SCORES",
                    "HISPANIC/LATINO MALES 5",
                    "HISPANIC/LATINO MALES 4",
                    "HISPANIC/LATINO MALES 3",
                    "HISPANIC/LATINO MALES 2",
                    "HISPANIC/LATINO MALES 1",
                    "HISPANIC/LATINO FEMALES 5",
                    "HISPANIC/LATINO FEMALES 4",
                    "HISPANIC/LATINO FEMALES 3",
                    "HISPANIC/LATINO FEMALES 2",
                    "HISPANIC/LATINO FEMALES 1"]]
```

Now that we have our columns, now I just need two specific rows. That is why I selected the "AP SCORES" column as well, because using this I can now select specific rows based on the values using the code written below:
```python:
calc_data = hisp_data[(hisp_data["AP SCORES"] == "CALCULUS AB") |
                 (hisp_data["AP SCORES"] == "CALCULUS BC")]
```
Now I am ready to analyze my data! I used the .describe() function to do some quick statistical summaries of each column. But to visualize it a little better, I did each column one at a time. 
```python:
print(round(calc_data["HISPANIC/LATINO MALES 5"].describe(),1))
print(round(calc_data["HISPANIC/LATINO MALES 4"].describe(),1))
print(round(calc_data["HISPANIC/LATINO MALES 3"].describe(),1))
print(round(calc_data["HISPANIC/LATINO MALES 2"].describe(),1))
print(round(calc_data["HISPANIC/LATINO MALES 1"].describe(),1))
```


```python:
# Prepare variables for the sums I need
males_passing_sum = 0
females_passing_sum = 0
males_failing_sum = 0
females_failing_sum = 0
total_students = 0

# *index* is the column race, gender, score. Such as: HISPANIC/LATINO MALES 5
# *value* is the number of tests with that race, gender, score
#for each race, gender, score combination
for index, value in calc_data.items():
    # if the column is female
    if "FEMALES" in index:
        # if the column is a passing test
        if "5" in index or "4" in index or "3" in index:
            #add to the female passing sum
            females_passing_sum += value
        else:
            # add to the female failing sum
            females_failing_sum += value
    elif "MALES" in index:
        if "5" in index or "4" in index or "3" in index:
            males_passing_sum += value
        else:
            males_failing_sum += value

total_students = males_passing_sum + males_failing_sum + females_passing_sum + females_failing_sum
print(total_students)

print()
print("For the AP Calculus Test")
print("___________________________")
print("Pass/Fail Totals:")
print("Total Males Passing: ", str(males_passing_sum))
print("Total Males Failing: ", str(males_failing_sum))
print("Total Females Passing: ", str(females_passing_sum))
print("Total Females Failing: ", str(females_failing_sum))
print()
```
```python:
print()
print("PERCENTAGES")
print("___________________________")
print("Students who passed:")
print("Total Males Passing (%): ", str((males_passing_sum/total_students) * 100))
print("Total Females Passing: ", str((females_passing_sum/total_students) * 100))
print()
```
