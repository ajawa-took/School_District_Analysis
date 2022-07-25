# School_District_Analysis
using pandas and jupyter notebooks

## Overview of the school district analysis

 Various performance metrics for the schools in the district were computed in two ways: with and without the reading and math scores of 9th-graders at Thomas High School. This analysis was motivated by the suspicion of some form of cheating on some or all of those tests.


## Results

 Effects of removing the test scores of 9th-graders at Thomas High School from our analysis.

 - All District Summary metrics decreased slightly, at the edge of visibility with the requested truncation. This is expected behaviour, regardless of potential cheating. Since this school performs far above the distric average, removing a random collection of Thomas High School students from the disctric pool would have this effect.


![District Results](/Results/whole-district-old.PNG)
![District Results after removals](/Results/whole-district.PNG)

 - School Summary metrics are, of course, unchanged for all other schools. For Thomas High School, four of the metrics went down very slightly, while the average reading score actually increased a little.

 - In the two By-School-By-Grade tables, the 9th-graders from Thomas High School make up one cell. Thus, dropping their test scores leaves that cell empty (filled with the null value NaN, to be more precise), and has no effect on other cells.

 - Thomas High School, with a budget of $638 per student, is in the second-highest spending range ($631-645) of our analysis. Taking the suspect test scores from that school out of our analysis again has miniscule effects on the performance metrics of that group. With the requested truncation, tiny decreases are visible for the passing rates for reading and overall, and no change is visible for the other two metrics. Of course, other groups' metrics are unchanged.

 - Thomas High School with its 1,635 students fits right in the middle of our range of medium-sized schools; so the metrics for small and large schools are not affected by the removal of some Thomas High School scores. For the group of medium-sized schools, the changes are again miniscule. The passing rate for reading went down from 96.8 to 96.7 with the removal of the suspect scores, and the other changes are too small to see.

 - Thomas High School is a charter school, so the performance metrics for disctrict schools were unchanged. For charter schools, dropping the suspect scores had no visible effect on any of the five metrics.


## Summary

 Four changes in the updated school district analysis after reading and math scores for the ninth grade at Thomas High School have been replaced with NaNs.

1. All district-wide metrics decreased slightly, as we removed better-perfoming students of a well-funded charter school from the overall sample.

2. Of course, we now have no performance metrics for 9th-graders at Thomas High School.

3. The performance metrics of Thomas High School itself changed very slightly, with 4 decreasing and 1 improving.

4. The performance metrics for the group of schools of size similar to Thomas High School, and for the group of schools with per capita funding similar to Thomas High School, decreased very slightly or stayed the same, as far as the truncated data shows.


## Methodology

 The .mean() method in pandas can do most, but not all, the cool sneaky things one might wish for. It will average a series of boolean values, treating True as 1 and False as 0, and return the percentage of True entries in the series. It drops null values from its computations. But when used on a column of booleans and nulls in conjunction with the groupby method, it ignores the whole column. Converting the whole column to numerical values fixes this issue with my sneaky way of completing this challenge, like so:

```
for colnam in ["pass_math", "pass_reading", "pass_both"]:
    school_data_complete_df[colnam] = pd.to_numeric(school_data_complete_df[colnam])
```

 The averages and passing rates for bins of several schools (by size, by type, and by spending per student) are not actual averages of the scores of the students in the schools in the bins. The proposed methodology first computes averages for each school, and then averages those results, meaning that students from smaller school contribute disproportionally to the final statistic. Why do we do this?

 The requested formatting truncates the data to the point where we cannot see the changes. This seems like a poor choice, both for the product (analysis) and for the process (learning pandas).

 Why do we include images rather than tables in our written reports?
