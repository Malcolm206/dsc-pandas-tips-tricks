# Pandas Tips & Review
### As a data scientist, you will be utilizing the pandas library in various ways to solve some of the world's most pressing issues

  
### Here are some useful pandas methods to manipulate dataframes to do and show us whatever we want!

![Alt Text](https://media.giphy.com/media/aUhEBE0T8XNHa/giphy.gif)

## Asking questions about the data

One of the most important skills to hone is to be able to ask intelligent questions about what a given dataset *is*, and then figure out *what questions that dataset can answer*.

Import `Absenteeism_at_work.csv` (which is in the same `dir` as this notebook) with a delimiter of `;`.  (IOW, each value of the data is separated by a semicolon in the csv file)

(No I don't know why we still call it a csv)

Answer the following questions below (and remember to *ask* them of *each* dataset you encounter!!!!:


- What does a "row" represent in this dataset?  
   - Is it a person?  Is it an event?  Is it an aggregated unit, like a neighborhood or a state?  
   
   
- What does each column represent?
   - Does it represent inherent characteristics?  Does it record things that happened? 
   
   - Which columns do you *know* what is represented?  Which columns require *assumptions*? (Often, you'll work with data that has poor / no documentation, and reasonable inferences have to be made about what the hell you're looking at)
   
   - 1 universally indicates "the presence of something"
     - eg in `Social Drinker`, `1` indicates "yes", `0` "no"
     - **unless** the column is representing a categorical variable w/ two values
       - eg in column like `sex`, `1` doesn't equal "yes"
   
   
- What are the data types in each column?
   - Are they strings?  Integers, floats?  Dates?  A mix?
   
   
- What are some columns that can be *engineered* from the columns that are given?   
   
- What are some questions you can ask that can be answered by this dataset?


```python

absent = pd.read_csv('Absenteeism_at_work.csv', delimiter=";")
print(absent.head())

print(absent.info())
```

       ID  Reason for absence  Month of absence  Day of the week  Seasons  \
    0  11                  26                 7                3        1   
    1  36                   0                 7                3        1   
    2   3                  23                 7                4        1   
    3   7                   7                 7                5        1   
    4  11                  23                 7                5        1   
    
       Transportation expense  Distance from Residence to Work  Service time  Age  \
    0                     289                               36            13   33   
    1                     118                               13            18   50   
    2                     179                               51            18   38   
    3                     279                                5            14   39   
    4                     289                               36            13   33   
    
       Work load Average/day   Hit target  Disciplinary failure  Education  Son  \
    0                 239.554          97                     0          1    2   
    1                 239.554          97                     1          1    1   
    2                 239.554          97                     0          1    0   
    3                 239.554          97                     0          1    2   
    4                 239.554          97                     0          1    2   
    
       Social drinker  Social smoker  Pet  Weight  Height  Body mass index  \
    0               1              0    1      90     172               30   
    1               1              0    0      98     178               31   
    2               1              0    0      89     170               31   
    3               1              1    0      68     168               24   
    4               1              0    1      90     172               30   
    
       Absenteeism time in hours  
    0                          4  
    1                          0  
    2                          2  
    3                          4  
    4                          2  
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 740 entries, 0 to 739
    Data columns (total 21 columns):
    ID                                 740 non-null int64
    Reason for absence                 740 non-null int64
    Month of absence                   740 non-null int64
    Day of the week                    740 non-null int64
    Seasons                            740 non-null int64
    Transportation expense             740 non-null int64
    Distance from Residence to Work    740 non-null int64
    Service time                       740 non-null int64
    Age                                740 non-null int64
    Work load Average/day              740 non-null float64
    Hit target                         740 non-null int64
    Disciplinary failure               740 non-null int64
    Education                          740 non-null int64
    Son                                740 non-null int64
    Social drinker                     740 non-null int64
    Social smoker                      740 non-null int64
    Pet                                740 non-null int64
    Weight                             740 non-null int64
    Height                             740 non-null int64
    Body mass index                    740 non-null int64
    Absenteeism time in hours          740 non-null int64
    dtypes: float64(1), int64(20)
    memory usage: 121.5 KB
    None


## Pandas Display Settings

Notice how the columns and rows are truncated?  Let's work on fixing this using pandas display settings!

## Selecting data

Do the following:


- select the column `Transportation expense`
  - what kind of object is a column?
  
  
- select all the rows in which `Distance from Residence to Work` is greater than 1,000 miles

- find the range of values inside `Distance from Residence to Work`

- select all the rows with a higher `Distance from Residence to Work` than the median

- man it's a pain in the ass to keep typing out `Distance from Residence to Work`, let's rename that column `commute_distance`

- select all the rows that have the modal value of `commute_distance`


```python

for obj in [
    absent['Transportation expense'],
    type(absent['Transportation expense']),
    absent['Distance from Residence to Work'].value_counts(),
    absent[
        absent['Distance from Residence to Work'] 
        >
        absent['Distance from Residence to Work']
        .median()
    ]
]:
    print(obj)
    print()
    
absent.rename(
    columns={
        'Distance from Residence to Work': 
        'commute_distance'
    },
    inplace=True
)


commute = absent['commute_distance']

mask = (commute == commute.mode()[0])

absent[mask]
```

    0      289
    1      118
    2      179
    3      279
    4      289
    5      179
    6      361
    7      260
    8      155
    9      235
          ... 
    730    189
    731    118
    732    361
    733    225
    734    369
    735    289
    736    235
    737    118
    738    231
    739    179
    Name: Transportation expense, Length: 740, dtype: int64
    
    <class 'pandas.core.series.Series'>
    
    26    128
    51    120
    10     55
    25     54
    50     45
    36     40
    31     37
    13     34
    12     29
    11     26
    16     26
    52     24
    22     20
    20     19
    17     15
    29     14
    15      9
    14      9
    49      8
    27      7
    42      7
    5       6
    48      5
    35      2
    45      1
    Name: Distance from Residence to Work, dtype: int64
    
         ID  Reason for absence  Month of absence  Day of the week  Seasons  \
    0    11                  26                 7                3        1   
    2     3                  23                 7                4        1   
    4    11                  23                 7                5        1   
    5     3                  23                 7                6        1   
    6    10                  22                 7                6        1   
    7    20                  23                 7                6        1   
    10   20                   1                 7                2        1   
    11   20                   1                 7                3        1   
    12   20                  11                 7                4        1   
    13    3                  11                 7                4        1   
    ..   ..                 ...               ...              ...      ...   
    714   2                   0                 6                2        3   
    718  15                  28                 6                5        3   
    721  12                  22                 6                5        1   
    724  12                  22                 6                4        1   
    726  12                  19                 7                6        1   
    730   6                  22                 7                3        1   
    732  10                  22                 7                4        1   
    735  11                  14                 7                3        1   
    738   8                   0                 0                4        2   
    739  35                   0                 0                6        3   
    
         Transportation expense  Distance from Residence to Work  Service time  \
    0                       289                               36            13   
    2                       179                               51            18   
    4                       289                               36            13   
    5                       179                               51            18   
    6                       361                               52             3   
    7                       260                               50            11   
    10                      260                               50            11   
    11                      260                               50            11   
    12                      260                               50            11   
    13                      179                               51            18   
    ..                      ...                              ...           ...   
    714                     235                               29            12   
    718                     291                               31            12   
    721                     233                               51             1   
    724                     233                               51             1   
    726                     233                               51             1   
    730                     189                               29            13   
    732                     361                               52             3   
    735                     289                               36            13   
    738                     231                               35            14   
    739                     179                               45            14   
    
         Age  Work load Average/day   Hit target  Disciplinary failure  Education  \
    0     33                 239.554          97                     0          1   
    2     38                 239.554          97                     0          1   
    4     33                 239.554          97                     0          1   
    5     38                 239.554          97                     0          1   
    6     28                 239.554          97                     0          1   
    7     36                 239.554          97                     0          1   
    10    36                 239.554          97                     0          1   
    11    36                 239.554          97                     0          1   
    12    36                 239.554          97                     0          1   
    13    38                 239.554          97                     0          1   
    ..   ...                     ...         ...                   ...        ...   
    714   48                 275.089          96                     1          1   
    718   40                 275.089          96                     0          1   
    721   31                 275.089          96                     0          2   
    724   31                 275.089          96                     0          2   
    726   31                 264.604          93                     0          2   
    730   33                 264.604          93                     0          1   
    732   28                 264.604          93                     0          1   
    735   33                 264.604          93                     0          1   
    738   39                 271.219          95                     0          1   
    739   53                 271.219          95                     0          1   
    
         Son  Social drinker  Social smoker  Pet  Weight  Height  Body mass index  \
    0      2               1              0    1      90     172               30   
    2      0               1              0    0      89     170               31   
    4      2               1              0    1      90     172               30   
    5      0               1              0    0      89     170               31   
    6      1               1              0    4      80     172               27   
    7      4               1              0    0      65     168               23   
    10     4               1              0    0      65     168               23   
    11     4               1              0    0      65     168               23   
    12     4               1              0    0      65     168               23   
    13     0               1              0    0      89     170               31   
    ..   ...             ...            ...  ...     ...     ...              ...   
    714    1               0              1    5      88     163               33   
    718    1               1              0    1      73     171               25   
    721    1               1              0    8      68     178               21   
    724    1               1              0    8      68     178               21   
    726    1               1              0    8      68     178               21   
    730    2               0              0    2      69     167               25   
    732    1               1              0    4      80     172               27   
    735    2               1              0    1      90     172               30   
    738    2               1              0    2     100     170               35   
    739    1               0              0    1      77     175               25   
    
         Absenteeism time in hours  
    0                            4  
    2                            2  
    4                            2  
    5                            2  
    6                            8  
    7                            4  
    10                           8  
    11                           8  
    12                           8  
    13                           1  
    ..                         ...  
    714                          0  
    718                          2  
    721                          8  
    724                          3  
    726                          2  
    730                         16  
    732                          8  
    735                          8  
    738                          0  
    739                          0  
    
    [310 rows x 21 columns]
    





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ID</th>
      <th>Reason for absence</th>
      <th>Month of absence</th>
      <th>Day of the week</th>
      <th>Seasons</th>
      <th>Transportation expense</th>
      <th>commute_distance</th>
      <th>Service time</th>
      <th>Age</th>
      <th>Work load Average/day</th>
      <th>Hit target</th>
      <th>Disciplinary failure</th>
      <th>Education</th>
      <th>Son</th>
      <th>Social drinker</th>
      <th>Social smoker</th>
      <th>Pet</th>
      <th>Weight</th>
      <th>Height</th>
      <th>Body mass index</th>
      <th>Absenteeism time in hours</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>51</td>
      <td>29</td>
      <td>0</td>
      <td>9</td>
      <td>2</td>
      <td>4</td>
      <td>225</td>
      <td>26</td>
      <td>9</td>
      <td>28</td>
      <td>241.476</td>
      <td>92</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>69</td>
      <td>169</td>
      <td>24</td>
      <td>0</td>
    </tr>
    <tr>
      <td>52</td>
      <td>28</td>
      <td>23</td>
      <td>9</td>
      <td>3</td>
      <td>4</td>
      <td>225</td>
      <td>26</td>
      <td>9</td>
      <td>28</td>
      <td>241.476</td>
      <td>92</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>69</td>
      <td>169</td>
      <td>24</td>
      <td>2</td>
    </tr>
    <tr>
      <td>56</td>
      <td>28</td>
      <td>18</td>
      <td>9</td>
      <td>4</td>
      <td>4</td>
      <td>225</td>
      <td>26</td>
      <td>9</td>
      <td>28</td>
      <td>241.476</td>
      <td>92</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>69</td>
      <td>169</td>
      <td>24</td>
      <td>3</td>
    </tr>
    <tr>
      <td>65</td>
      <td>22</td>
      <td>23</td>
      <td>10</td>
      <td>5</td>
      <td>4</td>
      <td>179</td>
      <td>26</td>
      <td>9</td>
      <td>30</td>
      <td>253.465</td>
      <td>93</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>56</td>
      <td>171</td>
      <td>19</td>
      <td>1</td>
    </tr>
    <tr>
      <td>67</td>
      <td>28</td>
      <td>23</td>
      <td>10</td>
      <td>6</td>
      <td>4</td>
      <td>225</td>
      <td>26</td>
      <td>9</td>
      <td>28</td>
      <td>253.465</td>
      <td>93</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>69</td>
      <td>169</td>
      <td>24</td>
      <td>3</td>
    </tr>
    <tr>
      <td>69</td>
      <td>28</td>
      <td>23</td>
      <td>10</td>
      <td>4</td>
      <td>4</td>
      <td>225</td>
      <td>26</td>
      <td>9</td>
      <td>28</td>
      <td>253.465</td>
      <td>93</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>69</td>
      <td>169</td>
      <td>24</td>
      <td>2</td>
    </tr>
    <tr>
      <td>73</td>
      <td>28</td>
      <td>23</td>
      <td>10</td>
      <td>4</td>
      <td>4</td>
      <td>225</td>
      <td>26</td>
      <td>9</td>
      <td>28</td>
      <td>253.465</td>
      <td>93</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>69</td>
      <td>169</td>
      <td>24</td>
      <td>3</td>
    </tr>
    <tr>
      <td>76</td>
      <td>28</td>
      <td>28</td>
      <td>10</td>
      <td>3</td>
      <td>4</td>
      <td>225</td>
      <td>26</td>
      <td>9</td>
      <td>28</td>
      <td>253.465</td>
      <td>93</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>69</td>
      <td>169</td>
      <td>24</td>
      <td>2</td>
    </tr>
    <tr>
      <td>81</td>
      <td>28</td>
      <td>23</td>
      <td>11</td>
      <td>4</td>
      <td>4</td>
      <td>225</td>
      <td>26</td>
      <td>9</td>
      <td>28</td>
      <td>306.345</td>
      <td>93</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>69</td>
      <td>169</td>
      <td>24</td>
      <td>1</td>
    </tr>
    <tr>
      <td>88</td>
      <td>28</td>
      <td>23</td>
      <td>11</td>
      <td>4</td>
      <td>4</td>
      <td>225</td>
      <td>26</td>
      <td>9</td>
      <td>28</td>
      <td>306.345</td>
      <td>93</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>69</td>
      <td>169</td>
      <td>24</td>
      <td>1</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>684</td>
      <td>22</td>
      <td>27</td>
      <td>5</td>
      <td>6</td>
      <td>3</td>
      <td>179</td>
      <td>26</td>
      <td>9</td>
      <td>30</td>
      <td>237.656</td>
      <td>99</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>56</td>
      <td>171</td>
      <td>19</td>
      <td>2</td>
    </tr>
    <tr>
      <td>689</td>
      <td>22</td>
      <td>27</td>
      <td>5</td>
      <td>4</td>
      <td>3</td>
      <td>179</td>
      <td>26</td>
      <td>9</td>
      <td>30</td>
      <td>237.656</td>
      <td>99</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>56</td>
      <td>171</td>
      <td>19</td>
      <td>2</td>
    </tr>
    <tr>
      <td>696</td>
      <td>28</td>
      <td>6</td>
      <td>5</td>
      <td>4</td>
      <td>3</td>
      <td>225</td>
      <td>26</td>
      <td>9</td>
      <td>28</td>
      <td>237.656</td>
      <td>99</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>69</td>
      <td>169</td>
      <td>24</td>
      <td>3</td>
    </tr>
    <tr>
      <td>700</td>
      <td>22</td>
      <td>27</td>
      <td>5</td>
      <td>6</td>
      <td>3</td>
      <td>179</td>
      <td>26</td>
      <td>9</td>
      <td>30</td>
      <td>237.656</td>
      <td>99</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>56</td>
      <td>171</td>
      <td>19</td>
      <td>2</td>
    </tr>
    <tr>
      <td>705</td>
      <td>28</td>
      <td>11</td>
      <td>5</td>
      <td>2</td>
      <td>3</td>
      <td>225</td>
      <td>26</td>
      <td>9</td>
      <td>28</td>
      <td>237.656</td>
      <td>99</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>69</td>
      <td>169</td>
      <td>24</td>
      <td>1</td>
    </tr>
    <tr>
      <td>707</td>
      <td>22</td>
      <td>27</td>
      <td>6</td>
      <td>4</td>
      <td>3</td>
      <td>179</td>
      <td>26</td>
      <td>9</td>
      <td>30</td>
      <td>275.089</td>
      <td>96</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>56</td>
      <td>171</td>
      <td>19</td>
      <td>3</td>
    </tr>
    <tr>
      <td>713</td>
      <td>22</td>
      <td>27</td>
      <td>6</td>
      <td>6</td>
      <td>3</td>
      <td>179</td>
      <td>26</td>
      <td>9</td>
      <td>30</td>
      <td>275.089</td>
      <td>96</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>56</td>
      <td>171</td>
      <td>19</td>
      <td>2</td>
    </tr>
    <tr>
      <td>717</td>
      <td>22</td>
      <td>13</td>
      <td>6</td>
      <td>5</td>
      <td>3</td>
      <td>179</td>
      <td>26</td>
      <td>9</td>
      <td>30</td>
      <td>275.089</td>
      <td>96</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>56</td>
      <td>171</td>
      <td>19</td>
      <td>2</td>
    </tr>
    <tr>
      <td>719</td>
      <td>22</td>
      <td>13</td>
      <td>6</td>
      <td>2</td>
      <td>1</td>
      <td>179</td>
      <td>26</td>
      <td>9</td>
      <td>30</td>
      <td>275.089</td>
      <td>96</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>56</td>
      <td>171</td>
      <td>19</td>
      <td>3</td>
    </tr>
    <tr>
      <td>733</td>
      <td>28</td>
      <td>22</td>
      <td>7</td>
      <td>4</td>
      <td>1</td>
      <td>225</td>
      <td>26</td>
      <td>9</td>
      <td>28</td>
      <td>264.604</td>
      <td>93</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>69</td>
      <td>169</td>
      <td>24</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
<p>128 rows × 21 columns</p>
</div>



## Working with multiple dataframes

#### One way to combine two datasets together is to use the the merge function from pandas

Let's take a look at the `.merge()` documentation in pandas before we begin [pandas.DataFrame.merge](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.merge.html)

We'll start with new datasets


```python

#merge df1 and df2, first method
merged_df1 = df1.merge(df2, left_index=True, right_index=True)
merged_df1.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>sex</th>
      <th>cp</th>
      <th>trestbps</th>
      <th>chol</th>
      <th>fbs</th>
      <th>restecg</th>
      <th>thalach</th>
      <th>exang</th>
      <th>oldpeak</th>
      <th>slope</th>
      <th>ca</th>
      <th>thal</th>
      <th>target</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>52</td>
      <td>1</td>
      <td>0</td>
      <td>125</td>
      <td>212</td>
      <td>0</td>
      <td>1</td>
      <td>168</td>
      <td>0</td>
      <td>1.0</td>
      <td>2</td>
      <td>2</td>
      <td>3</td>
      <td>0</td>
      <td>23</td>
      <td>39</td>
      <td>55</td>
    </tr>
    <tr>
      <td>1</td>
      <td>53</td>
      <td>1</td>
      <td>0</td>
      <td>140</td>
      <td>203</td>
      <td>1</td>
      <td>0</td>
      <td>155</td>
      <td>1</td>
      <td>3.1</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>90</td>
      <td>40</td>
      <td>4</td>
    </tr>
    <tr>
      <td>2</td>
      <td>70</td>
      <td>1</td>
      <td>0</td>
      <td>145</td>
      <td>174</td>
      <td>0</td>
      <td>1</td>
      <td>125</td>
      <td>1</td>
      <td>2.6</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>25</td>
      <td>74</td>
      <td>45</td>
    </tr>
    <tr>
      <td>3</td>
      <td>61</td>
      <td>1</td>
      <td>0</td>
      <td>148</td>
      <td>203</td>
      <td>0</td>
      <td>1</td>
      <td>161</td>
      <td>0</td>
      <td>0.0</td>
      <td>2</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>37</td>
      <td>31</td>
      <td>16</td>
    </tr>
    <tr>
      <td>4</td>
      <td>62</td>
      <td>0</td>
      <td>0</td>
      <td>138</td>
      <td>294</td>
      <td>1</td>
      <td>1</td>
      <td>106</td>
      <td>0</td>
      <td>1.9</td>
      <td>1</td>
      <td>3</td>
      <td>2</td>
      <td>0</td>
      <td>93</td>
      <td>10</td>
      <td>21</td>
    </tr>
  </tbody>
</table>
</div>




```python

#merge df1 and df2, second method
merged_df = pd.merge(df1, df2, left_index=True, right_index=True)
merged_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>sex</th>
      <th>cp</th>
      <th>trestbps</th>
      <th>chol</th>
      <th>fbs</th>
      <th>restecg</th>
      <th>thalach</th>
      <th>exang</th>
      <th>oldpeak</th>
      <th>slope</th>
      <th>ca</th>
      <th>thal</th>
      <th>target</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>52</td>
      <td>1</td>
      <td>0</td>
      <td>125</td>
      <td>212</td>
      <td>0</td>
      <td>1</td>
      <td>168</td>
      <td>0</td>
      <td>1.0</td>
      <td>2</td>
      <td>2</td>
      <td>3</td>
      <td>0</td>
      <td>54</td>
      <td>63</td>
      <td>84</td>
    </tr>
    <tr>
      <th>1</th>
      <td>53</td>
      <td>1</td>
      <td>0</td>
      <td>140</td>
      <td>203</td>
      <td>1</td>
      <td>0</td>
      <td>155</td>
      <td>1</td>
      <td>3.1</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>86</td>
      <td>26</td>
      <td>59</td>
    </tr>
    <tr>
      <th>2</th>
      <td>70</td>
      <td>1</td>
      <td>0</td>
      <td>145</td>
      <td>174</td>
      <td>0</td>
      <td>1</td>
      <td>125</td>
      <td>1</td>
      <td>2.6</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>79</td>
      <td>75</td>
      <td>84</td>
    </tr>
    <tr>
      <th>3</th>
      <td>61</td>
      <td>1</td>
      <td>0</td>
      <td>148</td>
      <td>203</td>
      <td>0</td>
      <td>1</td>
      <td>161</td>
      <td>0</td>
      <td>0.0</td>
      <td>2</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>12</td>
      <td>81</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>62</td>
      <td>0</td>
      <td>0</td>
      <td>138</td>
      <td>294</td>
      <td>1</td>
      <td>1</td>
      <td>106</td>
      <td>0</td>
      <td>1.9</td>
      <td>1</td>
      <td>3</td>
      <td>2</td>
      <td>0</td>
      <td>55</td>
      <td>99</td>
      <td>28</td>
    </tr>
  </tbody>
</table>
</div>



####  Another method to join two dataframes is to use the `.join` method

[pandas.DataFrame.join](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.join.html)

![](img/join-types.jpg)


```python

#join df1 and df2 w/ an inner join
joined_df = df1.join(df2, on=df1.age, how='inner')
joined_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>sex</th>
      <th>cp</th>
      <th>trestbps</th>
      <th>chol</th>
      <th>fbs</th>
      <th>restecg</th>
      <th>thalach</th>
      <th>exang</th>
      <th>oldpeak</th>
      <th>slope</th>
      <th>ca</th>
      <th>thal</th>
      <th>target</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>52</td>
      <td>1</td>
      <td>0</td>
      <td>125</td>
      <td>212</td>
      <td>0</td>
      <td>1</td>
      <td>168</td>
      <td>0</td>
      <td>1.0</td>
      <td>2</td>
      <td>2</td>
      <td>3</td>
      <td>0</td>
      <td>54</td>
      <td>63</td>
      <td>84</td>
    </tr>
    <tr>
      <th>1</th>
      <td>53</td>
      <td>1</td>
      <td>0</td>
      <td>140</td>
      <td>203</td>
      <td>1</td>
      <td>0</td>
      <td>155</td>
      <td>1</td>
      <td>3.1</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>86</td>
      <td>26</td>
      <td>59</td>
    </tr>
    <tr>
      <th>2</th>
      <td>70</td>
      <td>1</td>
      <td>0</td>
      <td>145</td>
      <td>174</td>
      <td>0</td>
      <td>1</td>
      <td>125</td>
      <td>1</td>
      <td>2.6</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>79</td>
      <td>75</td>
      <td>84</td>
    </tr>
    <tr>
      <th>3</th>
      <td>61</td>
      <td>1</td>
      <td>0</td>
      <td>148</td>
      <td>203</td>
      <td>0</td>
      <td>1</td>
      <td>161</td>
      <td>0</td>
      <td>0.0</td>
      <td>2</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>12</td>
      <td>81</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>62</td>
      <td>0</td>
      <td>0</td>
      <td>138</td>
      <td>294</td>
      <td>1</td>
      <td>1</td>
      <td>106</td>
      <td>0</td>
      <td>1.9</td>
      <td>1</td>
      <td>3</td>
      <td>2</td>
      <td>0</td>
      <td>55</td>
      <td>99</td>
      <td>28</td>
    </tr>
  </tbody>
</table>
</div>



#### We can also join two dataframes using the `.concat` function.  This function allows us to add new rows to our dataframe or new columns.

[pandas.concat documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.concat.html)


```python

#adding new columns to dataframe using concat
df5 = pd.concat([merged_df, df4], axis=1)
df5.tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>sex</th>
      <th>cp</th>
      <th>trestbps</th>
      <th>chol</th>
      <th>fbs</th>
      <th>restecg</th>
      <th>thalach</th>
      <th>exang</th>
      <th>oldpeak</th>
      <th>slope</th>
      <th>ca</th>
      <th>thal</th>
      <th>target</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>Chemical_A</th>
      <th>Chemical_B</th>
      <th>Chemical_C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1020</th>
      <td>59</td>
      <td>1</td>
      <td>1</td>
      <td>140</td>
      <td>221</td>
      <td>0</td>
      <td>1</td>
      <td>164</td>
      <td>1</td>
      <td>0.0</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
      <td>58</td>
      <td>16</td>
      <td>5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1021</th>
      <td>60</td>
      <td>1</td>
      <td>0</td>
      <td>125</td>
      <td>258</td>
      <td>0</td>
      <td>0</td>
      <td>141</td>
      <td>1</td>
      <td>2.8</td>
      <td>1</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>86</td>
      <td>28</td>
      <td>16</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1022</th>
      <td>47</td>
      <td>1</td>
      <td>0</td>
      <td>110</td>
      <td>275</td>
      <td>0</td>
      <td>0</td>
      <td>118</td>
      <td>1</td>
      <td>1.0</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>32</td>
      <td>27</td>
      <td>15</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1023</th>
      <td>50</td>
      <td>0</td>
      <td>0</td>
      <td>110</td>
      <td>254</td>
      <td>0</td>
      <td>0</td>
      <td>159</td>
      <td>0</td>
      <td>0.0</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
      <td>6</td>
      <td>89</td>
      <td>26</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1024</th>
      <td>54</td>
      <td>1</td>
      <td>0</td>
      <td>120</td>
      <td>188</td>
      <td>0</td>
      <td>1</td>
      <td>113</td>
      <td>0</td>
      <td>1.4</td>
      <td>1</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>17</td>
      <td>11</td>
      <td>44</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python

#concat row
concat_data = pd.concat([df5, df6], axis=0)
concat_data.tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>sex</th>
      <th>cp</th>
      <th>trestbps</th>
      <th>chol</th>
      <th>fbs</th>
      <th>restecg</th>
      <th>thalach</th>
      <th>exang</th>
      <th>oldpeak</th>
      <th>slope</th>
      <th>ca</th>
      <th>thal</th>
      <th>target</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>Chemical_A</th>
      <th>Chemical_B</th>
      <th>Chemical_C</th>
      <th>threstbps</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1022</th>
      <td>47</td>
      <td>1</td>
      <td>0.0</td>
      <td>110.0</td>
      <td>275</td>
      <td>0</td>
      <td>0</td>
      <td>118</td>
      <td>1</td>
      <td>1.0</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>32</td>
      <td>27</td>
      <td>15</td>
      <td>71</td>
      <td>58</td>
      <td>79</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1023</th>
      <td>50</td>
      <td>0</td>
      <td>0.0</td>
      <td>110.0</td>
      <td>254</td>
      <td>0</td>
      <td>0</td>
      <td>159</td>
      <td>0</td>
      <td>0.0</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
      <td>6</td>
      <td>89</td>
      <td>26</td>
      <td>28</td>
      <td>38</td>
      <td>61</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1024</th>
      <td>54</td>
      <td>1</td>
      <td>0.0</td>
      <td>120.0</td>
      <td>188</td>
      <td>0</td>
      <td>1</td>
      <td>113</td>
      <td>0</td>
      <td>1.4</td>
      <td>1</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>17</td>
      <td>11</td>
      <td>44</td>
      <td>55</td>
      <td>78</td>
      <td>85</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>0</th>
      <td>54</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>276</td>
      <td>0</td>
      <td>1</td>
      <td>146</td>
      <td>0</td>
      <td>0.5</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>1</td>
      <td>25</td>
      <td>23</td>
      <td>40</td>
      <td>3</td>
      <td>43</td>
      <td>45</td>
      <td>150.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>72</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>212</td>
      <td>1</td>
      <td>0</td>
      <td>171</td>
      <td>0</td>
      <td>2.9</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>58</td>
      <td>84</td>
      <td>57</td>
      <td>84</td>
      <td>71</td>
      <td>92</td>
      <td>143.0</td>
    </tr>
  </tbody>
</table>
</div>



# Ways to utilize lambda functions
#### .map(), .apply(), .applymap()

The map() method only works on pandas series

The apply () method works on panda series and data frames

The applymap() method works on the entire pandas data frame where the input function is applied to every element individually. In other words, applymap() is appy() + map()!


```python

#create new age colum w/ map

new_age_map = df.age.map(lambda x: x * 10)
new_age_map.head()
```




    0    520
    1    530
    2    700
    3    610
    4    620
    Name: age, dtype: int64




```python


#create new age colum w/ apply

new_age_apply = df.age.apply(lambda x: x * 10)
new_age_apply.head()
```




    0    520
    1    530
    2    700
    3    610
    4    620
    Name: age, dtype: int64



Do these two dataframes equal the same thing?


```python

(new_age_map == new_age_apply).value_counts()
```




    True    1025
    Name: age, dtype: int64




```python

#apply that manipulation to the entire dataframe w/ applymap

apply_df = df.applymap(lambda x: x*10)
```

#### How else could we manipulate the 'age' column?


```python

apply_df['age'] = [age - 1 for age in apply_df['age']]
```

#### We can also use these functions on strings.  Let's add a column of patient names to our dataset and manipulate those using a lambda function!

Let's generate a column of names


```python

#replacing the spaces in each name with an _
df.name = df.name.map(lambda x: x.replace(" ", "_"))
df = df.applymap(lambda x: x*10)
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>sex</th>
      <th>cp</th>
      <th>trestbps</th>
      <th>chol</th>
      <th>fbs</th>
      <th>restecg</th>
      <th>thalach</th>
      <th>exang</th>
      <th>oldpeak</th>
      <th>slope</th>
      <th>ca</th>
      <th>thal</th>
      <th>target</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>520</td>
      <td>10</td>
      <td>0</td>
      <td>1250</td>
      <td>2120</td>
      <td>0</td>
      <td>10</td>
      <td>1680</td>
      <td>0</td>
      <td>10.0</td>
      <td>20</td>
      <td>20</td>
      <td>30</td>
      <td>0</td>
      <td>Amy_KennedyAmy_KennedyAmy_KennedyAmy_KennedyAm...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>530</td>
      <td>10</td>
      <td>0</td>
      <td>1400</td>
      <td>2030</td>
      <td>10</td>
      <td>0</td>
      <td>1550</td>
      <td>10</td>
      <td>31.0</td>
      <td>0</td>
      <td>0</td>
      <td>30</td>
      <td>0</td>
      <td>Felicia_HowardFelicia_HowardFelicia_HowardFeli...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>700</td>
      <td>10</td>
      <td>0</td>
      <td>1450</td>
      <td>1740</td>
      <td>0</td>
      <td>10</td>
      <td>1250</td>
      <td>10</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>30</td>
      <td>0</td>
      <td>Adam_MaxwellAdam_MaxwellAdam_MaxwellAdam_Maxwe...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>610</td>
      <td>10</td>
      <td>0</td>
      <td>1480</td>
      <td>2030</td>
      <td>0</td>
      <td>10</td>
      <td>1610</td>
      <td>0</td>
      <td>0.0</td>
      <td>20</td>
      <td>10</td>
      <td>30</td>
      <td>0</td>
      <td>Eric_MolinaEric_MolinaEric_MolinaEric_MolinaEr...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>620</td>
      <td>0</td>
      <td>0</td>
      <td>1380</td>
      <td>2940</td>
      <td>10</td>
      <td>10</td>
      <td>1060</td>
      <td>0</td>
      <td>19.0</td>
      <td>10</td>
      <td>30</td>
      <td>20</td>
      <td>0</td>
      <td>Diana_GardnerDiana_GardnerDiana_GardnerDiana_G...</td>
    </tr>
  </tbody>
</table>
</div>



## Groupby!!!!! 

The workhorse of aggregating data together and manipulating it

df.groupby([list of columns]) creates a "groupby object" that *aggregates* the data according to *the columns in the list*

Then, we can select specific columns in this groupby object and perform calculations on the aggregations

An example is below:

```
df.groupby(['sex', 'target'])['age'].mean()
```

Using the example:

The columns inside the parens of `groupby` are *the columns that are aggregated*
- Think "group together every second column value in every first column value"
- So in this example, the data is aggregated "for every `target` value in every `sex` value"

Then we *select specific columns in the groubpy object* to perform calculations on


- in this case, `age`
  - can we select multiple columns?  We can. with a list! Try out `[['age', 'trestbps']]`

Then we perform a calculation
- in this case, finding the mean




What kind of object is this?

How do we select the values?

How do we find the index?

How do we select a specific value?

Select multiple columns (ie in addition to `age`); what kind of object is this?  How can we make it easier to manipulate?


```python

age_mean_sex_target = df.groupby(['sex', 'target'])['age'].mean()

for obj in [
    type(age_mean_sex_target),
    age_mean_sex_target.index,
    age_mean_sex_target[0,0],
    df.groupby(['sex', 'target'])[['age', 'trestbps']].mean(),
    type(
        df.groupby(
            ['sex', 'target']
        )
        [['age', 'trestbps']]
        .mean()
    ),
    df.groupby(
    ['sex', 'target']
    )
    [['age', 'trestbps']]
    .mean()
    .reset_index()
]: 
    print(obj)
    print()
```

    <class 'pandas.core.series.Series'>
    
    MultiIndex([(0, 0),
                (0, 1),
                (1, 0),
                (1, 1)],
               names=['sex', 'target'])
    
    59.05813953488372
    
                      age    trestbps
    sex target                       
    0   0       59.058140  146.488372
        1       54.628319  128.836283
    1   0       56.050847  131.527845
        1       50.736667  129.553333
    
    <class 'pandas.core.frame.DataFrame'>
    
       sex  target        age    trestbps
    0    0       0  59.058140  146.488372
    1    0       1  54.628319  128.836283
    2    1       0  56.050847  131.527845
    3    1       1  50.736667  129.553333
    

