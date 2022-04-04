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

### Statistical Analysis
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

|Statistical|Old|New|Percentage Difference|
|-----|:-----:|-----|:-----:|
|Average Math Score|79.0|78.9|-0.1%|
|Average Reading Score|81.9|81.9|- <br />The difference is very slitghly (0.03)|
|% Passing Math|75|74.8|-0.2%|
|% Passing Reading|86|85.7|-0.3%|
|% Overall Passing|65|64.9|-0.1%|

> Note that the number of total student used in calculation is `new_total_student_count` = 38709, which is different from the displayed number of Total Student in the district summary.


Average reading score original = 81.87784018381414
Average reading score update = 81.85579580976001


### School Summary

+ How is the school summary affected?

<img src= https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/per_school_summary_with_total_student.png width="80%" height="80%"> <img src= https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/per_school_summary_without_9thgraders_count.png width="80%" height="80%">


### Thomas High School's performance
+ How does replacing the ninth graders’ math and reading scores affect Thomas High School’s performance relative to the other schools?

<img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Original_outputs/five_schools_top_original.png width="50%" height="50%">
<img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Updated_outputs/five_schools_top_updated.png width="50%" height="50%">

### Scores by Grade, School Spending, School Size, School Type
+ How does replacing the ninth-grade scores affect the following:
  + Math and reading scores by grade
#### Math

<img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Original_outputs/math_scores_by_grade_original.png width="30%" height="30%"> <img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Updated_outputs/math_scores_by_grade_updated.png width="30%" height="30%">

#### Reading
<img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Original_outputs/reading_scores_by_grade_original.png width="30%" height="30%"> <img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Updated_outputs/reading_scores_by_grade_updated.png width="30%" height="30%">




  + Scores by school spending

<img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Updated_outputs/spending_summary_updated.png to-be-put width="90%" height="90%">

  + Scores by school size

<img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Updated_outputs/school_size_summary_updated.png width="90%" height="90%">

  + Scores by school type

<img src=https://github.com/asama-w/School_District_Analysis/blob/main/Additional%20Images/Updated_outputs/type_summary_updated.png width="90%" height="90%">

## 4) Summary
