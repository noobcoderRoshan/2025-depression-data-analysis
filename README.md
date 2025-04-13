# 2025-depression-data-analysis

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import micropip
await micropip.install('seaborn')
import pandas as pd
df = pd.read_csv("Student Depression Dataset.csv")
print(df.head())
   id  Gender   Age           City Profession  Academic Pressure  \
0   2    Male  33.0  Visakhapatnam    Student                5.0   
1   8  Female  24.0      Bangalore    Student                2.0   
2  26    Male  31.0       Srinagar    Student                3.0   
3  30  Female  28.0       Varanasi    Student                3.0   
4  32  Female  25.0         Jaipur    Student                4.0   

   Work Pressure  CGPA  Study Satisfaction  Job Satisfaction  \
0            0.0  8.97                 2.0               0.0   
1            0.0  5.90                 5.0               0.0   
2            0.0  7.03                 5.0               0.0   
3            0.0  5.59                 2.0               0.0   
4            0.0  8.13                 3.0               0.0   

      Sleep Duration Dietary Habits   Degree  \
0          5-6 hours        Healthy  B.Pharm   
1          5-6 hours       Moderate      BSc   
2  Less than 5 hours        Healthy       BA   
3          7-8 hours       Moderate      BCA   
4          5-6 hours       Moderate   M.Tech   

  Have you ever had suicidal thoughts ?  Work/Study Hours  Financial Stress  \
0                                   Yes               3.0               1.0   
1                                    No               3.0               2.0   
2                                    No               9.0               1.0   
3                                   Yes               4.0               5.0   
4                                   Yes               1.0               1.0   

  Family History of Mental Illness  Depression  
0                               No           1  
1                              Yes           0  
2                              Yes           0  
3                              Yes           1  
4                               No           0  
df.describe()
id	Age	Academic Pressure	Work Pressure	CGPA	Study Satisfaction	Job Satisfaction	Work/Study Hours	Financial Stress	Depression
count	27901.000000	27901.000000	27901.000000	27901.000000	27901.000000	27901.000000	27901.000000	27901.000000	27898.000000	27901.000000
mean	70442.149421	25.822300	3.141214	0.000430	7.656104	2.943837	0.000681	7.156984	3.139867	0.585499
std	40641.175216	4.905687	1.381465	0.043992	1.470707	1.361148	0.044394	3.707642	1.437347	0.492645
min	2.000000	18.000000	0.000000	0.000000	0.000000	0.000000	0.000000	0.000000	1.000000	0.000000
25%	35039.000000	21.000000	2.000000	0.000000	6.290000	2.000000	0.000000	4.000000	2.000000	0.000000
50%	70684.000000	25.000000	3.000000	0.000000	7.770000	3.000000	0.000000	8.000000	3.000000	1.000000
75%	105818.000000	30.000000	4.000000	0.000000	8.920000	4.000000	0.000000	10.000000	4.000000	1.000000
max	140699.000000	59.000000	5.000000	5.000000	10.000000	5.000000	4.000000	12.000000	5.000000	1.000000
df.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 27901 entries, 0 to 27900
Data columns (total 18 columns):
 #   Column                                 Non-Null Count  Dtype  
---  ------                                 --------------  -----  
 0   id                                     27901 non-null  int64  
 1   Gender                                 27901 non-null  object 
 2   Age                                    27901 non-null  float64
 3   City                                   27901 non-null  object 
 4   Profession                             27901 non-null  object 
 5   Academic Pressure                      27901 non-null  float64
 6   Work Pressure                          27901 non-null  float64
 7   CGPA                                   27901 non-null  float64
 8   Study Satisfaction                     27901 non-null  float64
 9   Job Satisfaction                       27901 non-null  float64
 10  Sleep Duration                         27901 non-null  object 
 11  Dietary Habits                         27901 non-null  object 
 12  Degree                                 27901 non-null  object 
 13  Have you ever had suicidal thoughts ?  27901 non-null  object 
 14  Work/Study Hours                       27901 non-null  float64
 15  Financial Stress                       27898 non-null  float64
 16  Family History of Mental Illness       27901 non-null  object 
 17  Depression                             27901 non-null  int64  
dtypes: float64(8), int64(2), object(8)
memory usage: 3.0+ MB
df.isnull().sum()
id                                       0
Gender                                   0
Age                                      0
City                                     0
Profession                               0
Academic Pressure                        0
Work Pressure                            0
CGPA                                     0
Study Satisfaction                       0
Job Satisfaction                         0
Sleep Duration                           0
Dietary Habits                           0
Degree                                   0
Have you ever had suicidal thoughts ?    0
Work/Study Hours                         0
Financial Stress                         3
Family History of Mental Illness         0
Depression                               0
dtype: int64
gender distribution

import micropip
await micropip.install('seaborn')
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
print(df.columns)
Index(['id', 'Gender', 'Age', 'City', 'Profession', 'Academic Pressure',
       'Work Pressure', 'CGPA', 'Study Satisfaction', 'Job Satisfaction',
       'Sleep Duration', 'Dietary Habits', 'Degree',
       'Have you ever had suicidal thoughts ?', 'Work/Study Hours',
       'Financial Stress', 'Family History of Mental Illness', 'Depression'],
      dtype='object')
plt.figure(figsize=(5,5))
ax = sns.countplot(data=df, x="Gender")
ax.bar_label(ax.containers[0])
plt.show()

The chart shows the count of student depression cases categorized by gender. Here are the key observations:
Male Students: There are 15,547 reported cases of depression. Female Students: There are 12,354 reported cases of depression. Summary Males exhibit a higher count of depression cases compared to females. This data could indicate different prevalence rates or reporting behaviors between genders.

gp = df.groupby("Academic Pressure").agg({"Degree": "count"})
# Group by the "Degree" column and calculate the mean of "Academic Pressure"
degree_pressure = df.groupby("Degree")["Academic Pressure"].mean()

# Sort the results to find the degree with the highest academic pressure
degree_pressure_sorted = degree_pressure.sort_values(ascending=False)

# Display the results
print(degree_pressure_sorted)
Degree
Class 12    3.359375
ME          3.313514
PhD         3.224138
B.Pharm     3.186420
MBBS        3.155172
BHM         3.129730
BCA         3.126308
B.Ed        3.118907
MBA         3.113879
M.Pharm     3.113402
BA          3.110000
BE          3.091354
B.Com       3.083001
LLM         3.082988
B.Tech      3.078993
MD          3.071678
BBA         3.067529
MA          3.066176
B.Arch      3.063599
MSc         3.057143
LLB         3.050671
BSc         3.048423
M.Ed        3.045067
M.Tech      2.982387
M.Com       2.961853
MCA         2.952107
Others      2.942857
MHM         2.937173
Name: Academic Pressure, dtype: float64
The data indicates that Class 12 students experience the highest level of academic pressure, with a score of 3.359375. This could be attributed to their preparation for competitive exams and the transition from secondary education to higher studies, particularly for those in science streams.

Following Class 12, degrees like ME (Master of Engineering) and B.Tech have significant pressure scores, suggesting that students in these programs also face considerable academic demands. It's common for students from science backgrounds to pursue engineering or computer applications (like BCA), which can be intense and competitive, contributing to higher levels of pressure.

The trend continues with graduates from fields such as MBBS, B.Pharm, and other professional degrees, indicating a sustained level of pressure across various programs. The data reflects a hierarchy of academic pressure where the rigor of the curriculum and the competitiveness of the field play crucial roles, especially in STEM and health-related disciplines.

Conversely, degrees such as M.Tech, M.Com, MCA, and others score lower on the pressure scale, which may reflect a difference in the perceived demands, course structure, or student coping mechanisms in these programs. Overall, the findings highlight the varying degrees of academic pressure experienced by students across different educational pathways.

pivot_table = df.pivot_table(values='Depression', index='Age', aggfunc='mean')
plt.figure(figsize=(10, 8))
sns.heatmap(pivot_table, annot=True, cmap='coolwarm', cbar=True)
plt.title('Depression Levels by Age')
plt.xlabel('Age')
plt.ylabel('Depression Level')
plt.show()

Peak Levels: The highest depression levels occur at ages 18 (0.77), 19 (0.71), and 22 (0.6). Bump at Age 41: There’s a notable spike at age 41, where the depression level reaches the maximum value of 1. Lower Levels: After age 43, depression levels significantly decline, with many ages showing a depression level of 0. Trend: Generally, younger adults appear to report higher depression levels, which tends to decrease as age increases after a certain point.

print(df.columns)
Index(['id', 'Gender', 'Age', 'City', 'Profession', 'Academic Pressure',
       'Work Pressure', 'CGPA', 'Study Satisfaction', 'Job Satisfaction',
       'Sleep Duration', 'Dietary Habits', 'Degree',
       'Have you ever had suicidal thoughts ?', 'Work/Study Hours',
       'Financial Stress', 'Family History of Mental Illness', 'Depression'],
      dtype='object')
degree_work_pressure = df.groupby("Degree")["Work Pressure"].mean()


degree_work_pressure_sorted = degree_work_pressure.sort_values(ascending=False)


print(degree_work_pressure_sorted)
Degree
Class 12    0.001974
B.Arch      0.000000
M.Ed        0.000000
Others      0.000000
MSc         0.000000
MHM         0.000000
ME          0.000000
MD          0.000000
MCA         0.000000
MBBS        0.000000
MBA         0.000000
MA          0.000000
M.Tech      0.000000
M.Pharm     0.000000
M.Com       0.000000
B.Com       0.000000
LLM         0.000000
LLB         0.000000
BSc         0.000000
BHM         0.000000
BE          0.000000
BCA         0.000000
BBA         0.000000
BA          0.000000
B.Tech      0.000000
B.Pharm     0.000000
B.Ed        0.000000
PhD         0.000000
Name: Work Pressure, dtype: float64
here we see degree and workpressure

sns.boxplot(data = df, x = "CGPA")
plt.show()

# Group by the "Degree" column and calculate the mean of depression
degree_depression = df.groupby("Degree")["Depression"].mean()

# Sort the results to find the degree with the highest depression
degree_depression_sorted = degree_depression.sort_values(ascending=False)

# Display the results
print(degree_depression_sorted)
Degree
Class 12    0.707730
Others      0.600000
B.Arch      0.589310
BSc         0.588964
BBA         0.584770
MBBS        0.580460
BCA         0.571528
MSc         0.570588
B.Tech      0.568576
B.Com       0.566401
BHM         0.550270
PhD         0.547893
B.Ed        0.546867
BE          0.544861
M.Pharm     0.539519
MBA         0.539146
LLM         0.537344
MCA         0.535441
BA          0.535000
MA          0.533088
M.Com       0.531335
LLB         0.530551
ME          0.529730
B.Pharm     0.528395
MD          0.520979
MHM         0.518325
M.Tech      0.509785
M.Ed        0.505481
Name: Depression, dtype: float64
degree_depression = df.groupby("Degree")["Depression"].mean()
plt.figure(figsize=(10, 8))
degree_depression.plot.pie(autopct='%1.1f%%', startangle=90, cmap='viridis')
plt.title('Depression Levels by Degree')
plt.ylabel('')  
plt.show()

colors = ['red' if (x == degree_depression.max()) else 'grey' for x in degree_depression]

plt.figure(figsize=(10, 8))
degree_depression.plot.pie(autopct='%1.1f%%', startangle=90, colors=colors)
plt.title('Depression Levels by Degree')
plt.ylabel('')  
plt.show()

here we see depression in which course is most

Also depreson varries on financial condition also
