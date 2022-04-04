# Analysis of School District Data
## 1) Project Overview
### Purpose of the analysis
To help Maria, who is a chief data scientist for City school District, update the school district analysis that was found to contain altered grades for Thomas High School ninth graders, and providing the school district board with the updated school performance trends which can assist them in the budget allotments decision. 

The math and reading testing scores of 9th graders at Thomas High school will be replaced with NaNs, representing them as a missing data, while the rest of the data will be kept intact. The analysis will then be performed on this clean dataset to see how the school performances as well as the overall analysis are affected.
### Analysis Overview
The analysis of the school district is performed twice,
1. **On original datasets:** Including Reading and Math scores of every students in the analysis. <br /> The full version of code and analysis outputs can be found in `PyCitySchools.ipynb`
2. **On updated datasets: Excluding Reading and Math scores of 9th graders at Thomas High School and re-do the same analysis.** <br /> The full version of code and analysis outputs can be found in `PyCitySchools_challenge.ipynb`. <br /> (The project is focus on the updated data, please refer to this code for the final report)

### Resources
The analysis is done on the student fundings and standardized Math and Reading testing scores of each student in each schools in the dataset. The resources and tools for this analysis is shown in the followings;

- **Data sources:** located in the `Resources` folder are
    - `schools_complete.csv`
    - `students_complete.csv`

- **Programming language:** Python3
- **Software:** Jupyter Notebook
- **Library:** Pandas, Numpy


## 2) Updating School District Analysis
### 2.1) Replace Reading and Math Scores of 9th Graders at Thomas High School
As the evidence of academic dishonesty lies in the reading and math scores of 9th graders at Thomas High School, these scores will be replaced with NaNs to omit them from the statistical analysis. The clean-up will first be performed on the `student_data_df` dataframe. 

The outputs of the original and updated dataframes are shown below. Original dataframe (left), Updated dataframe (right) <br />In the blue highlighted row, this student is a 9th grader at Thomas High School, so his reading and math score has been replaced with NaN.

<img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Original_outputs/student_data_original.png width="45%" height="45%"> <img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Updated_outputs/student_data_updated.png width="45%" height="45%">

### 2.2) Perform School District Analysis of the Updated Data
After the reading and math scores of 9th graders at Thomas High School has been omited, this clean student dataframe is combined with `school_data_df` dataframe, creating the new dataframe `school_data_complete_df` where the analysis will be applied on. The overview of the dataframe is shown below. 

<img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/school_data_complete.png width="80%" height="80%">

### 2.3) Statistical Analysis
There are 5 calculations performed in this analysis to determine the trends of school performances:
+ Average Math Score
+ Average Reading Score
+ % Passing Math (Percentage of students who pass Math): Math scores higher than 70
+ % Passing Reading (Percentage of students who pass Reading): Reading scores higher than 70
+ % Overall Passing (Percentage of students who pass both Math and Reading): Math and Reading Scores higher than 70

All of the calculations depends on the total number of students who have the valid scores. When the scores of Thomas High School's 9th graders are excluded, the total number of students with scores will also be changed and the analysis needs to be re-done based on the new total student number:

||Number of Student|
|-----|:-----:|
|Original Total Student|39170|
|9th graders at Thomas High School|461|
|New Total Student (no THS[^1] 9th graders)|**38709**| 

[^1]:Note: THS = Thomas High School

Examples of the code calculating this statistics based on the new total student count `new_total_student_count` = 38709 
```python
average_math_score = school_data_complete_df["math_score"].mean()
passing_math_percentage = passing_math_count / float(new_total_student_count) * 100
overall_passing_percentage = overall_passing_math_reading_count / new_total_student_count * 100
```

## 3) Results
### District Summary 
The following images show the output of `district_summary_df` dataframe of the original data and the updated data, respectively. The updated data is highlighted in blue.

<img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Original_outputs/district_summary_original.png width="90%" height="90%">
<img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Updated_outputs/district_summary_update.png width="90%" height="90%">

Since the score values of THS 9th graders are NaNs, or no value, the total number of the scores used to calculate is reduced from 39170 to 38709, the updated district summary show slight decreases in all of the statistical analysis (only 0.1-0.3% lower than the original statistics), while the output of Total School, Total Student, and Total Budget remain the same as the information in the dataframe remains intact.

|Statistical|Old Analysis|New Analysis|Percentage Difference|
|-----|:-----:|-----|:-----:|
|Average Math Score|79.0|78.9|-0.1%|
|Average Reading Score|81.9|81.9|- <br />The difference is very slitghly (0.02)|
|% Passing Math|75|74.8|-0.2%|
|% Passing Reading|86|85.7|-0.3%|
|% Overall Passing|65|64.9|-0.1%|

> Note that the number of total student used in calculation is `new_total_student_count` = 38709, which is different from the displayed number of Total Student in the district summary.

### School Summary
This analysis is carried out per each school data, to compare the values between schools.
Similar to the district summary, the statistical calculations that involves the total number of students are affected when the Thomas High School's 9th graders are null, despite a very slightly changes in the percentage. The Total School Budget and Per Student Budget remains the same, as the altered data does not concern these two columns in this analysis.

Thomas High School data has a total of 1635 student in 9th-12th grade combined.
|Grade|Number of Student|variable in code preview|
|-----|:-----:|----|
|_9th_|_461_||
|10th|421||
|11th|415||
|12th|338||
|**Total (9th-12th graders) |1635**|`per_school_counts`|
|**New Total (only 10th-12th graders) |1174**|`THS_tenth_to_twelfth_graders_count`|

When excluding all the scores of 9th graders, meaning the statistics of the scores that are shown in the school summary dataframe are calculated from the data of 10th to 12th graders, where the total number of 10th-12th graders are 1174. 

However, after replacing the math and reading grades of Thomas High School 9th graders and use this data to calculate the statistics of Thomas High School based on the first-round analysis code, the % Passing Math, % Passing Reading, and % Overall Passing considerably drop to 60% range from being in 90% range in the original dataset. This is due to change in the total value of collected scores, which is lower compared to the original data as 461 scores set of the 9th graders cannot be included. Meanwhile, the percentage calculations per total students of each school still use the total number of student in the school, which is 1635, as a result, the percentages decline significantly.

Example of the code in determining the % Passing Overall using the total number student in the school (all grades), <br />`per_school_counts` = 1635

```python
# Retrieveing total number of student
per_school_counts = school_data_complete_df["school_name"].value_counts()
# Calculating % Passing Overall
per_overall_passing_percentage = per_passing_math_reading / per_school_counts * 100
```

To correct the statistic calculation, the number of students of which the scores are used in calculations are determined. Only the 10th to 12th graders students are counted for Thomas High School statistics. <br />`THS_tenth_to_twelfth_graders_count` = 1174

```python
# Number of 10th to 12th grader students
THS_tenth_to_twelfth_graders_count = THS_tenth_graders_count + THS_eleventh_graders_count + THS_twelfth_graders_count
# Calculating % Passing Overall
THS_overall_passing_percentage = THS_overall_passing_math_reading_count / THS_tenth_to_twelfth_graders_count * 100
```
As a result, the statistical analysis of Thomas High School in the lastest updated school summary now varies slightly lower by 0.1% from the original statistics. The following image shows the updated per school summary dataframe, with Thomas High School highlighed in blue.

<img src= https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/per_school_summary_without_9thgraders_count.png width="80%" height="80%">

The school summary output images of the original can be found here [Per School Summary (Original)](https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/per_school_summary_original.png) and the update with per_school_count can be found here [Per School Summary (THS total student count)](https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/per_school_summary_with_total_student.png) 


### Thomas High School's performance
Showing the top 5 schools, Thomas High School still remains in the second place, same place as in the original data output, with very slightly decrease by 1-3% in % Passing Math, Passing Reading and % Overall Passing, and slightly increase in average math and average reading score by 0.05%.

Replacing the ninth graders’ math and reading scores does not significantly affect Thomas High School’s performance relative to the other schools, as the updated statistics remain relatively close to the original statistics.

<img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Original_outputs/five_schools_top_original.png width="70%" height="70%">
<img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Updated_outputs/five_schools_top_updated.png width="70%" height="70%">

### Scores by Grade, School Spending, School Size, School Type
#### Math and Reading scores by grade
For both Math and Reading score by grade dataframe, after replacing the ninth graders’ math and reading scores, both updated dataframe show `nan` in the 9th grade cell of Thomas High School, representing the absent values of Thomas High School's 9th grader scores. The values in other rows and column remain the same.

+ **Math scores by grade** outputs of original (left) and updated (right) are shown in the following 

<img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Original_outputs/math_scores_by_grade_original.png width="30%" height="30%"> <img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Updated_outputs/math_scores_by_grade_updated.png width="30%" height="30%">
+ **Reading scores by grade** outputs of original (left) and updated (right) are shown in the following 

<img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Original_outputs/reading_scores_by_grade_original.png width="30%" height="30%"> <img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Updated_outputs/reading_scores_by_grade_updated.png width="30%" height="30%">

### Scores by school spending
Replacing NaNs for the ninth graders’ math and reading scores has no affected on the school spending summary dataframe, as the budget per student is calculated based on the total number of students in school (does not exclude student who doesn't have math and reading score) <br />`per_school_capita = per_school_budget / per_school_counts`

<img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Updated_outputs/spending_summary_updated.png to-be-put width="80%" height="80%">

### Scores by school size
Thomas High School still remains in the medium school size range as the total number of student in the school does not changed, only the 9th graders' scores are not included in the ststistical analysis.

<img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Updated_outputs/school_size_summary_updated.png width="80%" height="80%">

### Scores by school type
There are 2 school types, Charter and District. Thomas High School is in Charter type. <br />Omitting ninth grader's scores has no effect on the statistics by school type as the differences in the average scores and percentage passings are very small.

<img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Updated_outputs/type_summary_updated.png width="80%" height="80%">

## 4) Summary
Summary of the changes in the updated school analysis after replacing math and reading scores for ninth graders at Thomas High school:
+ In the district summary, total number of student count use to determine the passing percentage are reduced from 39170 students to 38709 students after omitting the 9th graders'scores.
+ In the district summary, where the statistics are calculated by number of students count in the district (only count the students who have valid math and reading scores), the average scores and the overall performance percentage slighly decline by less than 0.3%
+ In school summary (per school), where the the statistics are based on number of student in each school (with valid scores), the averages and performance percentages are also decrease by up to 0.3%
+ In school summary (per school), despite the slight decrease in other calculated statistics, only the average reading score shows a slight increase by 0.1% (from 83.8% to 83.9%) when the 9th graders are omitted. 
+ In the updated analysis, when calculating the passing percentage per school, the number of students whose scores are omitted should not be included in the calculations, otherwise the results will be much altered. For example, to calculate the overall percentage, the sum of the scores of 1174 students cannot be divided by the total number of 1635 students in school as there are 461 scores absent.
