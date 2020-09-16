# Pandas Tips & Review
### As a data scientist, you will be utilizing the pandas library in various ways to solve some of the world's most pressing issues

  
### Here are some useful pandas methods to manipulate dataframes to do and show us whatever we want!

![Alt Text](https://media.giphy.com/media/aUhEBE0T8XNHa/giphy.gif)

## Pandas Display Settings

Notice how the columns and rows are truncated?  Let's work on fixing this using pandas display settings!

## Working with multiple dataframes

#### One way to combine two datasets together is to use the the merge function from pandas

Let's take a look at the `.merge()` documentation in pandas before we begin [pandas.DataFrame.merge](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.merge.html)


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

#### We can also join two dataframes using the `.concat` function.  This function allows us to add new rows to our dataframe or new columns.

[pandas.concat documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.concat.html)

# Ways to utilize lambda functions
#### .map(), .apply(), .applymap()

The map() method only works on pandas series

The apply () method works on panda series and data frames

The applymap() method works on the entire pandas data frame where the input function is applied to every element individually. In other words, applymap() is appy() + map()!

Do these two dataframes equal the same thing?

#### How else could we manipulate the 'age' column?

#### We can also use these functions on strings.  Let's add a column of patient names to our dataset and manipulate those using a lambda function!

Let's generate a column of names

# Transposing Data

There are a variety of ways you might want to transpose your dataframe.  One thing you might want to do is turn columns into rows.  You can do this very easily using the `.transpose` or `.t` function.

[Pandas Transpose](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.transpose.html)

### Pivot tables which you might be familiar with are also possible to create in pandas using the `.pivot_table()` function

[pivot_table](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.pivot_table.html)

### Another way to view information across two or more factors is to create a cross tabulation using the pandas `.crosstab` function

[Pandas Crosstab](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.crosstab.html)

asdfhadj 
