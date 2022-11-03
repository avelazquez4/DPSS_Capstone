2022 Data and Policy Summer Scholar Program - Education Policy Capstone
Research Project
================
Anne Velazquez
2022-11-02

## Introduction

This capstone research project was completed as part of the 2022 Data
and Policy Summer Scholar Program (DPSS) held through the University of
Chicago Harris School of Public Policy.

The purpose of this analysis is to estimate the impact of the Safe
Passage Program, a public policy designed and introduced by the the City
of Chicago (see
[here](https://www.cps.edu/services-and-supports/student-safety-and-security/safe-passage-program/)
for more details on the program). The main purpose of the program is “to
provide a positive, trusted adult presence for students as they travel
to and from school.”

## Data Cleaning and Exploration

This project used the five datasets outlined below relating to the Safe
Passage Program, attendance rates at Chicago Public Schools and crime
statistics near these schools.

1.  “Attnd” (metrics_attendance_2021.xlsx): Attendance data for Chicago
    public schools. This dataset is publicly available and can be found
    [here](https://www.cps.edu/about/district-data/metrics/) under
    “Attendance over time”.

2.  “control” (“control.csv”): List of Chicago schools without the Safe
    Passage Program and geographic information

3.  “treatment” (“treated.csv”): List of Chicago schools with the Safe
    Passage Program, when it was implemented and geographic information

4.  “crimes” (“crime-data.csv”): Information on Chicago crimes within
    500 yards of schools including crime type, location, and date of
    crime.

5.  “schools_v\_crime” (“school-vs-crime-distances.csv”): Chicago crimes
    that happened within 500 yards of school and their distance from the
    relevant school(s)

### School Data

## intro this visual!!!!!!!!!!!!!!!!!

Let’s look at where the schools with the Safe Passage Program are
located compared to other schools in the Chicago area.

![Schools Map](SchoolsMap.png)

From the map of the treated schools compared to control schools, the
treated schools do *not* appear to be evenly distributed throughout the
Chicago area. Most schools with the safe passage program (treated) are
in the southern part of Chicago. There is a higher concentration of
treated schools near the South Side, New City, and Englewood areas
specifically. Treated schools generally appear more concentrated near
the center of the city and are less prevalent towards the edges of the
city.

### Crime Data

Now lets look at the Chicago crime data. The map below shows crimes from
2013-2018 that took place within a 50 yard distance from schools. Based
on the map, crimes appear more highly concentrated near the center of
the city.

[Crime Map](CrimeMap.png)

### School Attendance Data

SOME SORT OF CHART ON ATTENDANCE DATA

Given we have panel data across several years for various schools, there
may be unobserved variables impacting crimes or attendance that are
specific to the locations/schools being studied or to the time frame the
data was collected. To control for these time invariant and entity
invariant unobservable variables and better understand the impact of the
Safe Passage Program, we can use a fixed effects regression model with
‘School ID’ and ‘Year’ as fixed effects.

However, in order to use fixed effects regression analysis to produce an
unbiased estimate of the impact of the Safe Passage Program on crime
near schools, first we must confirm if the ‘parallel trends’ assumption
holds. In other words, we will confirm if crime rates near schools with
the Safe Passage Program were trending similarly to those without the
program prior to 2015 when the program was implemented. If this is true,
we can use fixed effects regression to analyze the impact of the
program.

First, lets evaluate the trends of crimes within 50 yards of schools.
The graph below shows that, on average, all schools had decreasing rates
of crime within 50 yards prior to 2015. After 2015, schools with the
Safe Passage Program continued to see nearby crime decrease on average
through 2018, while schools without the program saw nearby crimes
increase slightly and hold relatively flat through 2018. In short,
nearby crime rates were trending similarly at all schools before the the
Safe Passage Program was implemented in 2015, but not perfectly
parallel.

[Crimes 50
yards](https://github.com/avelazquez4/DPSS_Capstone/blob/main/ParallelTrends_Crime50.png?raw=true)

If instead we expand the radius to evaluate trends of crimes within 200
yards of schools, this appears to strengthen the parallel trends
assumption between schools with and without the Safe Passage Program

the trend of crime rates prior to 2015 appears more parallel between
schools with and without the Safe Passage Program compared to crimes
within 50 yards.

[Crimes 200 yards](ParallelTrends_Crime200.png)

Now look at trends for school attendance rates before and after the Safe
Passage Program went into effect. From the graph below, it does not look
like the parallel trend assumption holds for school attendance rates.
The schools that did implement the program had attendance rates trending
slightly upward prior to 2015, while control schools had fairly flat
attendance rates. Given the parallel trends assumption does not hold, we
cannot produce an unbiased estimation of the impact of the Safe Passage
Program on school attendance rates using a fixed effects regression
model.

[School Attendance Trends](ParallelTrends_Attend.png)

## Analysis and Results

Now, we can use a fixed effects regression model to determine if the
Safe Passage Program had a significant impact on crimes nearby to
schools.

*Run a fixed effects regression of total crime in the presence of the
Safe Passage Policy. It should also include both ‘school’ fixed effects
and ‘year’ fixed effects.*

[Crime Model](model_crime.html)

The coefficient for the indicator variable for the Safe Passage Program
has a p-value significant at the .001 level. This means that the Safe
Passage Program has a statistically significant relationship with the
rate of crimes within 50 yards of schools. By including fixed effects
for schools and each year in the model, we eliminate the risk of bias
due to omitted factors that vary across schools and that vary over time.

#### Part B

*Run the same regression as in (a), but now run of school attendance on
the presence of the Safe Passage Policy. *

INSERT STARGAZER HERE

*The coefficient for the indicator variable has a p-value significant at
the .001 level. This means that the Safe Passage Program has a
statistically significant relationship with school attendance rates.
However, there is likely bias in this model as the*

What further analysis should be done?

-   Did crime decrease overall or did the Safe Passage Program just
    shift crime to different areas/schools?
