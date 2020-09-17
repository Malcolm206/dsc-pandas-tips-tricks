# Pandas Tips & Review
### As a data scientist, you will be utilizing the pandas library in various ways to solve some of the world's most pressing issues

  
### Here are some useful pandas methods to manipulate dataframes to do and show us whatever we want!

![Alt Text](https://media.giphy.com/media/aUhEBE0T8XNHa/giphy.gif)


```python
import pandas as pd
import numpy as np
```

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

```

## Pandas Display Settings


```python
absent = pd.read_csv('Absenteeism_at_work.csv', delimiter=";")
absent
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
      <th>ID</th>
      <th>Reason for absence</th>
      <th>Month of absence</th>
      <th>Day of the week</th>
      <th>Seasons</th>
      <th>Transportation expense</th>
      <th>Distance from Residence to Work</th>
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
      <td>0</td>
      <td>11</td>
      <td>26</td>
      <td>7</td>
      <td>3</td>
      <td>1</td>
      <td>289</td>
      <td>36</td>
      <td>13</td>
      <td>33</td>
      <td>239.554</td>
      <td>97</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>90</td>
      <td>172</td>
      <td>30</td>
      <td>4</td>
    </tr>
    <tr>
      <td>1</td>
      <td>36</td>
      <td>0</td>
      <td>7</td>
      <td>3</td>
      <td>1</td>
      <td>118</td>
      <td>13</td>
      <td>18</td>
      <td>50</td>
      <td>239.554</td>
      <td>97</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>98</td>
      <td>178</td>
      <td>31</td>
      <td>0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>3</td>
      <td>23</td>
      <td>7</td>
      <td>4</td>
      <td>1</td>
      <td>179</td>
      <td>51</td>
      <td>18</td>
      <td>38</td>
      <td>239.554</td>
      <td>97</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>89</td>
      <td>170</td>
      <td>31</td>
      <td>2</td>
    </tr>
    <tr>
      <td>3</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>5</td>
      <td>1</td>
      <td>279</td>
      <td>5</td>
      <td>14</td>
      <td>39</td>
      <td>239.554</td>
      <td>97</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>68</td>
      <td>168</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <td>4</td>
      <td>11</td>
      <td>23</td>
      <td>7</td>
      <td>5</td>
      <td>1</td>
      <td>289</td>
      <td>36</td>
      <td>13</td>
      <td>33</td>
      <td>239.554</td>
      <td>97</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>90</td>
      <td>172</td>
      <td>30</td>
      <td>2</td>
    </tr>
    <tr>
      <td>5</td>
      <td>3</td>
      <td>23</td>
      <td>7</td>
      <td>6</td>
      <td>1</td>
      <td>179</td>
      <td>51</td>
      <td>18</td>
      <td>38</td>
      <td>239.554</td>
      <td>97</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>89</td>
      <td>170</td>
      <td>31</td>
      <td>2</td>
    </tr>
    <tr>
      <td>6</td>
      <td>10</td>
      <td>22</td>
      <td>7</td>
      <td>6</td>
      <td>1</td>
      <td>361</td>
      <td>52</td>
      <td>3</td>
      <td>28</td>
      <td>239.554</td>
      <td>97</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>4</td>
      <td>80</td>
      <td>172</td>
      <td>27</td>
      <td>8</td>
    </tr>
    <tr>
      <td>7</td>
      <td>20</td>
      <td>23</td>
      <td>7</td>
      <td>6</td>
      <td>1</td>
      <td>260</td>
      <td>50</td>
      <td>11</td>
      <td>36</td>
      <td>239.554</td>
      <td>97</td>
      <td>0</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>65</td>
      <td>168</td>
      <td>23</td>
      <td>4</td>
    </tr>
    <tr>
      <td>8</td>
      <td>14</td>
      <td>19</td>
      <td>7</td>
      <td>2</td>
      <td>1</td>
      <td>155</td>
      <td>12</td>
      <td>14</td>
      <td>34</td>
      <td>239.554</td>
      <td>97</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>95</td>
      <td>196</td>
      <td>25</td>
      <td>40</td>
    </tr>
    <tr>
      <td>9</td>
      <td>1</td>
      <td>22</td>
      <td>7</td>
      <td>2</td>
      <td>1</td>
      <td>235</td>
      <td>11</td>
      <td>14</td>
      <td>37</td>
      <td>239.554</td>
      <td>97</td>
      <td>0</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>88</td>
      <td>172</td>
      <td>29</td>
      <td>8</td>
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
      <td>730</td>
      <td>6</td>
      <td>22</td>
      <td>7</td>
      <td>3</td>
      <td>1</td>
      <td>189</td>
      <td>29</td>
      <td>13</td>
      <td>33</td>
      <td>264.604</td>
      <td>93</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>69</td>
      <td>167</td>
      <td>25</td>
      <td>16</td>
    </tr>
    <tr>
      <td>731</td>
      <td>34</td>
      <td>23</td>
      <td>7</td>
      <td>4</td>
      <td>1</td>
      <td>118</td>
      <td>10</td>
      <td>10</td>
      <td>37</td>
      <td>264.604</td>
      <td>93</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>83</td>
      <td>172</td>
      <td>28</td>
      <td>2</td>
    </tr>
    <tr>
      <td>732</td>
      <td>10</td>
      <td>22</td>
      <td>7</td>
      <td>4</td>
      <td>1</td>
      <td>361</td>
      <td>52</td>
      <td>3</td>
      <td>28</td>
      <td>264.604</td>
      <td>93</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>4</td>
      <td>80</td>
      <td>172</td>
      <td>27</td>
      <td>8</td>
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
    <tr>
      <td>734</td>
      <td>13</td>
      <td>13</td>
      <td>7</td>
      <td>2</td>
      <td>1</td>
      <td>369</td>
      <td>17</td>
      <td>12</td>
      <td>31</td>
      <td>264.604</td>
      <td>93</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>70</td>
      <td>169</td>
      <td>25</td>
      <td>80</td>
    </tr>
    <tr>
      <td>735</td>
      <td>11</td>
      <td>14</td>
      <td>7</td>
      <td>3</td>
      <td>1</td>
      <td>289</td>
      <td>36</td>
      <td>13</td>
      <td>33</td>
      <td>264.604</td>
      <td>93</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>90</td>
      <td>172</td>
      <td>30</td>
      <td>8</td>
    </tr>
    <tr>
      <td>736</td>
      <td>1</td>
      <td>11</td>
      <td>7</td>
      <td>3</td>
      <td>1</td>
      <td>235</td>
      <td>11</td>
      <td>14</td>
      <td>37</td>
      <td>264.604</td>
      <td>93</td>
      <td>0</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>88</td>
      <td>172</td>
      <td>29</td>
      <td>4</td>
    </tr>
    <tr>
      <td>737</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>1</td>
      <td>118</td>
      <td>14</td>
      <td>13</td>
      <td>40</td>
      <td>271.219</td>
      <td>95</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>8</td>
      <td>98</td>
      <td>170</td>
      <td>34</td>
      <td>0</td>
    </tr>
    <tr>
      <td>738</td>
      <td>8</td>
      <td>0</td>
      <td>0</td>
      <td>4</td>
      <td>2</td>
      <td>231</td>
      <td>35</td>
      <td>14</td>
      <td>39</td>
      <td>271.219</td>
      <td>95</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>100</td>
      <td>170</td>
      <td>35</td>
      <td>0</td>
    </tr>
    <tr>
      <td>739</td>
      <td>35</td>
      <td>0</td>
      <td>0</td>
      <td>6</td>
      <td>3</td>
      <td>179</td>
      <td>45</td>
      <td>14</td>
      <td>53</td>
      <td>271.219</td>
      <td>95</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>77</td>
      <td>175</td>
      <td>25</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>740 rows × 21 columns</p>
</div>



Notice how the columns and rows are truncated?  Let's work on fixing this using pandas display settings!


```python
#viewing our current settings
print(pd.options.display.max_columns)
print(pd.options.display.max_rows)
```

    50
    20



```python
#adjusting settings
pd.options.display.max_columns = 50
pd.options.display.min_rows = 20
```


```python
#reviewing our settings
print(pd.options.display.max_columns)
print(pd.options.display.min_rows)
```

    50
    20



```python
#checking our dataframe again to see if our settings worked
absent
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
      <th>ID</th>
      <th>Reason for absence</th>
      <th>Month of absence</th>
      <th>Day of the week</th>
      <th>Seasons</th>
      <th>Transportation expense</th>
      <th>Distance from Residence to Work</th>
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
      <td>0</td>
      <td>11</td>
      <td>26</td>
      <td>7</td>
      <td>3</td>
      <td>1</td>
      <td>289</td>
      <td>36</td>
      <td>13</td>
      <td>33</td>
      <td>239.554</td>
      <td>97</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>90</td>
      <td>172</td>
      <td>30</td>
      <td>4</td>
    </tr>
    <tr>
      <td>1</td>
      <td>36</td>
      <td>0</td>
      <td>7</td>
      <td>3</td>
      <td>1</td>
      <td>118</td>
      <td>13</td>
      <td>18</td>
      <td>50</td>
      <td>239.554</td>
      <td>97</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>98</td>
      <td>178</td>
      <td>31</td>
      <td>0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>3</td>
      <td>23</td>
      <td>7</td>
      <td>4</td>
      <td>1</td>
      <td>179</td>
      <td>51</td>
      <td>18</td>
      <td>38</td>
      <td>239.554</td>
      <td>97</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>89</td>
      <td>170</td>
      <td>31</td>
      <td>2</td>
    </tr>
    <tr>
      <td>3</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>5</td>
      <td>1</td>
      <td>279</td>
      <td>5</td>
      <td>14</td>
      <td>39</td>
      <td>239.554</td>
      <td>97</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>68</td>
      <td>168</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <td>4</td>
      <td>11</td>
      <td>23</td>
      <td>7</td>
      <td>5</td>
      <td>1</td>
      <td>289</td>
      <td>36</td>
      <td>13</td>
      <td>33</td>
      <td>239.554</td>
      <td>97</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>90</td>
      <td>172</td>
      <td>30</td>
      <td>2</td>
    </tr>
    <tr>
      <td>5</td>
      <td>3</td>
      <td>23</td>
      <td>7</td>
      <td>6</td>
      <td>1</td>
      <td>179</td>
      <td>51</td>
      <td>18</td>
      <td>38</td>
      <td>239.554</td>
      <td>97</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>89</td>
      <td>170</td>
      <td>31</td>
      <td>2</td>
    </tr>
    <tr>
      <td>6</td>
      <td>10</td>
      <td>22</td>
      <td>7</td>
      <td>6</td>
      <td>1</td>
      <td>361</td>
      <td>52</td>
      <td>3</td>
      <td>28</td>
      <td>239.554</td>
      <td>97</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>4</td>
      <td>80</td>
      <td>172</td>
      <td>27</td>
      <td>8</td>
    </tr>
    <tr>
      <td>7</td>
      <td>20</td>
      <td>23</td>
      <td>7</td>
      <td>6</td>
      <td>1</td>
      <td>260</td>
      <td>50</td>
      <td>11</td>
      <td>36</td>
      <td>239.554</td>
      <td>97</td>
      <td>0</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>65</td>
      <td>168</td>
      <td>23</td>
      <td>4</td>
    </tr>
    <tr>
      <td>8</td>
      <td>14</td>
      <td>19</td>
      <td>7</td>
      <td>2</td>
      <td>1</td>
      <td>155</td>
      <td>12</td>
      <td>14</td>
      <td>34</td>
      <td>239.554</td>
      <td>97</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>95</td>
      <td>196</td>
      <td>25</td>
      <td>40</td>
    </tr>
    <tr>
      <td>9</td>
      <td>1</td>
      <td>22</td>
      <td>7</td>
      <td>2</td>
      <td>1</td>
      <td>235</td>
      <td>11</td>
      <td>14</td>
      <td>37</td>
      <td>239.554</td>
      <td>97</td>
      <td>0</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>88</td>
      <td>172</td>
      <td>29</td>
      <td>8</td>
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
      <td>730</td>
      <td>6</td>
      <td>22</td>
      <td>7</td>
      <td>3</td>
      <td>1</td>
      <td>189</td>
      <td>29</td>
      <td>13</td>
      <td>33</td>
      <td>264.604</td>
      <td>93</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>69</td>
      <td>167</td>
      <td>25</td>
      <td>16</td>
    </tr>
    <tr>
      <td>731</td>
      <td>34</td>
      <td>23</td>
      <td>7</td>
      <td>4</td>
      <td>1</td>
      <td>118</td>
      <td>10</td>
      <td>10</td>
      <td>37</td>
      <td>264.604</td>
      <td>93</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>83</td>
      <td>172</td>
      <td>28</td>
      <td>2</td>
    </tr>
    <tr>
      <td>732</td>
      <td>10</td>
      <td>22</td>
      <td>7</td>
      <td>4</td>
      <td>1</td>
      <td>361</td>
      <td>52</td>
      <td>3</td>
      <td>28</td>
      <td>264.604</td>
      <td>93</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>4</td>
      <td>80</td>
      <td>172</td>
      <td>27</td>
      <td>8</td>
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
    <tr>
      <td>734</td>
      <td>13</td>
      <td>13</td>
      <td>7</td>
      <td>2</td>
      <td>1</td>
      <td>369</td>
      <td>17</td>
      <td>12</td>
      <td>31</td>
      <td>264.604</td>
      <td>93</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>70</td>
      <td>169</td>
      <td>25</td>
      <td>80</td>
    </tr>
    <tr>
      <td>735</td>
      <td>11</td>
      <td>14</td>
      <td>7</td>
      <td>3</td>
      <td>1</td>
      <td>289</td>
      <td>36</td>
      <td>13</td>
      <td>33</td>
      <td>264.604</td>
      <td>93</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>90</td>
      <td>172</td>
      <td>30</td>
      <td>8</td>
    </tr>
    <tr>
      <td>736</td>
      <td>1</td>
      <td>11</td>
      <td>7</td>
      <td>3</td>
      <td>1</td>
      <td>235</td>
      <td>11</td>
      <td>14</td>
      <td>37</td>
      <td>264.604</td>
      <td>93</td>
      <td>0</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>88</td>
      <td>172</td>
      <td>29</td>
      <td>4</td>
    </tr>
    <tr>
      <td>737</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>1</td>
      <td>118</td>
      <td>14</td>
      <td>13</td>
      <td>40</td>
      <td>271.219</td>
      <td>95</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>8</td>
      <td>98</td>
      <td>170</td>
      <td>34</td>
      <td>0</td>
    </tr>
    <tr>
      <td>738</td>
      <td>8</td>
      <td>0</td>
      <td>0</td>
      <td>4</td>
      <td>2</td>
      <td>231</td>
      <td>35</td>
      <td>14</td>
      <td>39</td>
      <td>271.219</td>
      <td>95</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>100</td>
      <td>170</td>
      <td>35</td>
      <td>0</td>
    </tr>
    <tr>
      <td>739</td>
      <td>35</td>
      <td>0</td>
      <td>0</td>
      <td>6</td>
      <td>3</td>
      <td>179</td>
      <td>45</td>
      <td>14</td>
      <td>53</td>
      <td>271.219</td>
      <td>95</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>77</td>
      <td>175</td>
      <td>25</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>740 rows × 21 columns</p>
</div>



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

```

## Working with multiple dataframes

#### One way to combine two datasets together is to use the the merge function from pandas

Let's take a look at the `.merge()` documentation in pandas before we begin [pandas.DataFrame.merge](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.merge.html)

We'll start with new datasets


```python
df1 = pd.read_csv('heart.csv')
df1.head()
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
    </tr>
  </tbody>
</table>
</div>




```python
df2 = pd.DataFrame(np.random.randint(0,100,size=(1025,3)), columns=['B','C','D'])
df2.head()
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
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>44</td>
      <td>52</td>
      <td>18</td>
    </tr>
    <tr>
      <td>1</td>
      <td>91</td>
      <td>43</td>
      <td>58</td>
    </tr>
    <tr>
      <td>2</td>
      <td>29</td>
      <td>90</td>
      <td>54</td>
    </tr>
    <tr>
      <td>3</td>
      <td>62</td>
      <td>41</td>
      <td>94</td>
    </tr>
    <tr>
      <td>4</td>
      <td>97</td>
      <td>7</td>
      <td>31</td>
    </tr>
  </tbody>
</table>
</div>




```python
#merge df1 and df2

```


```python
#merge df1 and df2 through a different method

```

####  Another method to join two dataframes is to use the `.join` method

[pandas.DataFrame.join](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.join.html)

![](img/join-types.jpg)


```python
#join df1 and df2 w/ an inner join


```

#### We can also join two dataframes using the `.concat` function.  This function allows us to add new rows to our dataframe or new columns.

[pandas.concat documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.concat.html)


```python
# creating a new dataframe with columns
df4 = pd.DataFrame(np.random.randint(0,100,size=(1000,3)), columns=['Chemical_A','Chemical_B','Chemical_C'])
df4.head()
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
      <th>Chemical_A</th>
      <th>Chemical_B</th>
      <th>Chemical_C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>25</td>
      <td>58</td>
      <td>37</td>
    </tr>
    <tr>
      <th>1</th>
      <td>90</td>
      <td>79</td>
      <td>88</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>35</td>
      <td>45</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7</td>
      <td>60</td>
      <td>56</td>
    </tr>
    <tr>
      <th>4</th>
      <td>99</td>
      <td>74</td>
      <td>41</td>
    </tr>
  </tbody>
</table>
</div>




```python

```


```python
#adding new columns to dataframe using concat

```


```python
#creating a new row

df6 = pd.DataFrame({'age':[54, 72], 'sex':[1,0], "threstbps":[150, 143], 'chol':[276, 212], \
                    'fbs':[0, 1], 'restecg': [1, 0], 'thalach':[146, 171], 'exang':[0, 0], \
                    'oldpeak': [0.5, 2.9], 'slope':[1, 2], "ca" :[2, 0], "thal":[2, 2], \
                    "target": [1, 0], 'B':[25, 58], "C":[23, 84], "D":[40, 57], "Chemical_A":[3, 84], \
                    "Chemical_B":[43, 71], "Chemical_C": [45, 92]})
df6
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
      <th>threstbps</th>
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
      <th>0</th>
      <td>54</td>
      <td>1</td>
      <td>150</td>
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
    </tr>
    <tr>
      <th>1</th>
      <td>72</td>
      <td>0</td>
      <td>143</td>
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
    </tr>
  </tbody>
</table>
</div>




```python
#concat row

```

# Ways to utilize lambda functions
#### .map(), .apply(), .applymap()

The map() method only works on pandas series

The apply () method works on panda series and data frames

The applymap() method works on the entire pandas data frame where the input function is applied to every element individually. In other words, applymap() is appy() + map()!


```python
df = pd.read_csv('heart.csv')
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
    </tr>
  </tbody>
</table>
</div>




```python
#create new age colum w/ map

```


```python
#create new age colum w/ apply

```

Do these two dataframes equal the same thing?


```python

```


```python
#apply that manipulation we did to ind. columns to the entire dataframe w/ applymap

```


```python
apply_df.head()
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
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
    </tr>
    <tr>
      <td>1</td>
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
    </tr>
    <tr>
      <td>2</td>
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
    </tr>
    <tr>
      <td>3</td>
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
    </tr>
    <tr>
      <td>4</td>
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
    </tr>
  </tbody>
</table>
</div>



#### How else could we manipulate the 'age' column?


```python

```

#### We can also use these functions on strings.  Let's add a column of patient names to our dataset and manipulate those using a lambda function!


```python
!pip install faker
```

    Requirement already satisfied: faker in /anaconda3/lib/python3.7/site-packages (4.0.1)
    Requirement already satisfied: python-dateutil>=2.4 in /anaconda3/lib/python3.7/site-packages (from faker) (2.8.1)
    Requirement already satisfied: text-unidecode==1.3 in /anaconda3/lib/python3.7/site-packages (from faker) (1.3)
    Requirement already satisfied: six>=1.5 in /anaconda3/lib/python3.7/site-packages (from python-dateutil>=2.4->faker) (1.14.0)



```python
from faker import Faker
fake = Faker()
fake.name()
```




    'Mark Mcknight'



Let's generate a column of names


```python
#creating patient names
df['name'] = [fake.name() for x in range(1025)]
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
      <td>Amy Kennedy</td>
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
      <td>Felicia Howard</td>
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
      <td>Adam Maxwell</td>
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
      <td>Eric Molina</td>
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
      <td>Diana Gardner</td>
    </tr>
  </tbody>
</table>
</div>




```python
#apply that manipulation to the entire dataframe w/ applymap


```

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





```python
df.groupby(['sex', 'target'])['age'].mean()
```




    sex  target
    0    0         59.058140
         1         54.628319
    1    0         56.050847
         1         50.736667
    Name: age, dtype: float64



What kind of object is this?

How do we select the values?

How do we find the index?

How do we select a specific value?

Select multiple columns (ie in addition to `age`); what kind of object is this?  How can we make it easier to manipulate?


```python

```
