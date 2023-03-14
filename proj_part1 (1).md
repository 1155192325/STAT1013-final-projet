---
jupyter:
  colab:
    toc_visible: true
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 0
---

<div class="cell markdown" id="9xZnRXM7x0Cv">

# CUHK-STAT1013: Practical Assignment Part 1: Sharing Your Idea and Data

</div>

<div class="cell markdown" id="9Fy05KAkyJI0">

## Sleep efficiency dataset background

**Description**:

Dataset describing the sleeping pattern of tested individual from
different background.

**Kaggle**:
<https://www.kaggle.com/datasets/equilibriumm/sleep-efficiency>

**Sample size**: 452

**Feature documentation**:

| Feature                | Dtype   |
|:-----------------------|:--------|
| ID                     | int64   |
| Age                    | int64   |
| Gender                 | object  |
| Bedtime                | object  |
| Wakeup time            | object  |
| Sleep duration         | float64 |
| Sleep efficiency       | float64 |
| REM sleep percentage   | int64   |
| Deep sleep percentage  | int64   |
| Light sleep percentage | int64   |
| Awakenings             | float64 |
| Caffeine consumption   | float64 |
| Alcohol consumption    | float64 |
| Smoking status         | object  |
| Exercise frequency     | float64 |

</div>

<div class="cell markdown" id="k85zO7zxys4H">

## Hypothesis

-   Tell us what your idea is and why you have chosen to pursue this
    idea.
    -   We are interested in "*Did non-smokers have better sleep
        efficiency than smokers?*" We found that nowaday many modern
        humans suffer from insomnia, and we know that smoking causes
        many harms to our health. Therefore, we want to investigate the
        relationship between bad living habit like smoking and insonmia.
-   What two groups you are comparing:
    -   **G1**: Sleep efficiency of smoker ; **G2**: Sleep efficiency of
        non-smoker
-   What you will be measuring (i.e., what your response variable will
    be)
    -   `Sleep Efficiency`
-   Is your response variable quantitative rather than categorical?
    -   `Sleep Efficiency` is the measure of the proportion of time in
        bed spent asleep, which is between 0 and 1 and can be regarded
        as a quantitative variable.
-   Make a prediction about what kind of difference you expect to see
    between your samples and WHY.
    -   We'd expect that **G2** \> **G1** since cigarette contain
        nicotine which is a stimulant. [Smoke at night and sleep worse?
        The associations between cigarette smoking with insomnia
        severity and sleep
        duration](https://pubmed.ncbi.nlm.nih.gov/33221256/)
-   Talk about how you will gather your data
    -   From Kaggle link:
        <https://www.kaggle.com/datasets/equilibriumm/sleep-efficiency>
-   If you had unlimited resources (time, money, staff, etc.) how would
    you collect your data?
    -   \(i\) Use simple random sampling to choose sample. ; (ii) Give
        every tested individual a sleeptracker watch to measure their
        sleep effucuency.

</div>

<div class="cell markdown" id="3GOdPWT03PQB">

## Prepare your dataset

</div>

<div class="cell code" execution_count="37"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:478}"
id="mUxJb4hxvpHQ" outputId="28402709-70cf-4e53-9f7c-e8b0b3f653c7">

``` python
## load dataset from github

import pandas as pd

df = pd.read_csv('/content/Sleep_Efficiency.csv')
df.head(5)
```

<div class="output execute_result" execution_count="37">

       ID  Age  Gender              Bedtime          Wakeup time  Sleep duration  \
    0   1   65  Female  2021-03-06 01:00:00  2021-03-06 07:00:00             6.0   
    1   2   69    Male  2021-12-05 02:00:00  2021-12-05 09:00:00             7.0   
    2   3   40  Female  2021-05-25 21:30:00  2021-05-25 05:30:00             8.0   
    3   4   40  Female  2021-11-03 02:30:00  2021-11-03 08:30:00             6.0   
    4   5   57    Male  2021-03-13 01:00:00  2021-03-13 09:00:00             8.0   

       Sleep efficiency  REM sleep percentage  Deep sleep percentage  \
    0              0.88                    18                     70   
    1              0.66                    19                     28   
    2              0.89                    20                     70   
    3              0.51                    23                     25   
    4              0.76                    27                     55   

       Light sleep percentage  Awakenings  Caffeine consumption  \
    0                      12         0.0                   0.0   
    1                      53         3.0                   0.0   
    2                      10         1.0                   0.0   
    3                      52         3.0                  50.0   
    4                      18         3.0                   0.0   

       Alcohol consumption Smoking status  Exercise frequency  
    0                  0.0            Yes                 3.0  
    1                  3.0            Yes                 3.0  
    2                  0.0             No                 3.0  
    3                  5.0            Yes                 1.0  
    4                  3.0             No                 3.0  

</div>

</div>

<div class="cell markdown" id="55xAIxVa3hpQ">

-   Tell us what groups you want to compare in the dataset
    -   **G1** (sleep efficiency \| Smoking status = yes) vs. **G2**
        (sleep efficiency \| Smoking status = no)

</div>

<div class="cell markdown" id="13PdL3ht3902">

-   Print first 5 records of each group, respectively.

</div>

<div class="cell code" execution_count="7"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="UNL0WXav3hLj" outputId="36f5c75c-fb7c-42b7-e078-5a9639187fc4">

``` python
## First 5 records of G1 (smoker)
(df[df['Smoking status'] == 'Yes']['Sleep efficiency']).head(5)
```

<div class="output execute_result" execution_count="7">

    0    0.88
    1    0.66
    3    0.51
    6    0.54
    7    0.90
    Name: Sleep efficiency, dtype: float64

</div>

</div>

<div class="cell code" execution_count="17"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="dhe52HVB4T1O" outputId="81295ff5-3751-4420-dae5-f4f0d73436ed">

``` python
## First 5 records of G2 (non-smoker)
(df[df['Smoking status'] == 'No']['Sleep efficiency']).head(5)
```

<div class="output execute_result" execution_count="17">

    2    0.89
    4    0.76
    5    0.90
    8    0.79
    9    0.55
    Name: Sleep efficiency, dtype: float64

</div>

</div>

<div class="cell code" execution_count="38"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="zEgfWXaKGvNC" outputId="41e02546-a765-4f8a-e627-9942d1f65dab">

``` python
## Any other data description and visualization you want to add.
## Open question, be flexible and no example can be provided.
df.info()
```

<div class="output stream stdout">

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 452 entries, 0 to 451
    Data columns (total 15 columns):
     #   Column                  Non-Null Count  Dtype  
    ---  ------                  --------------  -----  
     0   ID                      452 non-null    int64  
     1   Age                     452 non-null    int64  
     2   Gender                  452 non-null    object 
     3   Bedtime                 452 non-null    object 
     4   Wakeup time             452 non-null    object 
     5   Sleep duration          452 non-null    float64
     6   Sleep efficiency        452 non-null    float64
     7   REM sleep percentage    452 non-null    int64  
     8   Deep sleep percentage   452 non-null    int64  
     9   Light sleep percentage  452 non-null    int64  
     10  Awakenings              432 non-null    float64
     11  Caffeine consumption    427 non-null    float64
     12  Alcohol consumption     438 non-null    float64
     13  Smoking status          452 non-null    object 
     14  Exercise frequency      446 non-null    float64
    dtypes: float64(6), int64(5), object(4)
    memory usage: 53.1+ KB

</div>

</div>

<div class="cell code" execution_count="39"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:809}"
id="qGkHHiQ4tytc" outputId="8edcd048-cd46-4429-afa2-173bda027b34">

``` python
df.describe(include='all').T
```

<div class="output execute_result" execution_count="39">

                            count unique                  top freq       mean  \
    ID                      452.0    NaN                  NaN  NaN      226.5   
    Age                     452.0    NaN                  NaN  NaN  40.285398   
    Gender                    452      2                 Male  228        NaN   
    Bedtime                   452    424  2021-03-11 01:00:00    3        NaN   
    Wakeup time               452    434  2021-11-25 06:00:00    2        NaN   
    Sleep duration          452.0    NaN                  NaN  NaN   7.465708   
    Sleep efficiency        452.0    NaN                  NaN  NaN   0.788916   
    REM sleep percentage    452.0    NaN                  NaN  NaN  22.615044   
    Deep sleep percentage   452.0    NaN                  NaN  NaN  52.823009   
    Light sleep percentage  452.0    NaN                  NaN  NaN  24.561947   
    Awakenings              432.0    NaN                  NaN  NaN   1.641204   
    Caffeine consumption    427.0    NaN                  NaN  NaN  23.653396   
    Alcohol consumption     438.0    NaN                  NaN  NaN   1.173516   
    Smoking status            452      2                   No  298        NaN   
    Exercise frequency      446.0    NaN                  NaN  NaN    1.79148   

                                   std   min     25%    50%     75%    max  
    ID                      130.625419   1.0  113.75  226.5  339.25  452.0  
    Age                       13.17225   9.0    29.0   40.0    52.0   69.0  
    Gender                         NaN   NaN     NaN    NaN     NaN    NaN  
    Bedtime                        NaN   NaN     NaN    NaN     NaN    NaN  
    Wakeup time                    NaN   NaN     NaN    NaN     NaN    NaN  
    Sleep duration            0.866625   5.0     7.0    7.5     8.0   10.0  
    Sleep efficiency          0.135237   0.5  0.6975   0.82     0.9   0.99  
    REM sleep percentage      3.525963  15.0    20.0   22.0    25.0   30.0  
    Deep sleep percentage    15.654235  18.0   48.25   58.0    63.0   75.0  
    Light sleep percentage   15.313665   7.0    15.0   18.0    32.5   63.0  
    Awakenings                1.356762   0.0     1.0    1.0     3.0    4.0  
    Caffeine consumption     30.202785   0.0     0.0   25.0    50.0  200.0  
    Alcohol consumption       1.621377   0.0     0.0    0.0     2.0    5.0  
    Smoking status                 NaN   NaN     NaN    NaN     NaN    NaN  
    Exercise frequency        1.428134   0.0     0.0    2.0     3.0    5.0  

</div>

</div>

<div class="cell code" execution_count="35"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="J_FvlMKit6EP" outputId="83f45bde-a03a-43ee-f537-8792be366d39">

``` python
print("number of smoker:" )
print(len(df[df['Smoking status'] == 'Yes']))
```

<div class="output stream stdout">

    number of smoker:
    154

</div>

</div>

<div class="cell code" execution_count="40"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:749}"
id="94iRYEhyxnxH" outputId="8cbb7edc-010b-4c48-8bb4-6ee738e9f1c1">

``` python
import seaborn as sns
import matplotlib.pyplot as plt
sns.histplot(data=df,x='Smoking status', y='Sleep efficiency')
plt.show()

sns.violinplot(data=df, x="Smoking status", y='Sleep efficiency')
plt.show()

g = sns.FacetGrid (df,col='Gender')
g.map(sns.histplot,'Smoking status','Sleep efficiency')
plt.show()

```

<div class="output display_data">

![](812765fdfeb6cac54f2458abaa57f6035f79b5de.png)

</div>

<div class="output display_data">

![](2fa0405e28630f2041494a575f33783dd929916e.png)

</div>

<div class="output display_data">

![](e83f4139532b3c2af226c57caf9de4ebbbdad634.png)

</div>

</div>
