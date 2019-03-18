## Heroes of Pymoli

![Fantasy](Images/Fantasy.jpg)

Congratulations! After a lot of hard work in the data munging mines, you've landed a job as Lead Analyst for an independent gaming company. You've been assigned the task of analyzing the data for their most recent fantasy game Heroes of Pymoli.

Like many others in its genre, the game is free-to-play, but players are encouraged to purchase optional items that enhance their playing experience. As a first task, the company would like you to generate a report that breaks down the game's purchasing data into meaningful insights.

Your final report should include each of the following:

### Player Count

* Total Number of Players

### Purchasing Analysis (Total)

* Number of Unique Items
* Average Purchase Price
* Total Number of Purchases
* Total Revenue

### Gender Demographics

* Percentage and Count of Male Players
* Percentage and Count of Female Players
* Percentage and Count of Other / Non-Disclosed

### Purchasing Analysis (Gender)

* The below each broken by gender
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Average Purchase Total per Person by Gender

### Age Demographics

* The below each broken into bins of 4 years (i.e. &lt;10, 10-14, 15-19, etc.)
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Average Purchase Total per Person by Age Group

### Top Spenders

* Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
  * SN
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value

### Most Popular Items

* Identify the 5 most popular items by purchase count, then list (in a table):
  * Item ID
  * Item Name
  * Purchase Count
  * Item Price
  * Total Purchase Value

### Most Profitable Items

* Identify the 5 most profitable items by total purchase value, then list (in a table):
  * Item ID
  * Item Name
  * Purchase Count
  * Item Price
  * Total Purchase Value

### Heroes Of Pymoli Data Analysis

* Although just 14% of the players are female, they have spent more then the male player by average. Female players have spent S4.47 and male players have spent S4.07.


* Players between 35-39 years old have spent more than the other age categories by average, S4.76.


* The top 4 popular items average cost is greater than the total items average cost and the top 5 profitable items also have an averagr cost greater than the total items average cost



```python
# Dependencies and Setup
import pandas as pd
import numpy as np
import os

# Input File path
input_file = os.path.join("Resources","purchase_data.csv")

# Read Purchasing File and store into Pandas data frame
df_purchase_data = pd.read_csv(input_file)

# Display first 5 rows
df_purchase_data.head()
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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Verify number of rows for each column
# Verify if some information is missing
df_purchase_data.count()
# There is no missing information
```




    Purchase ID    780
    SN             780
    Age            780
    Gender         780
    Item ID        780
    Item Name      780
    Price          780
    dtype: int64



## Player Count

* Total number of players



```python
# Calculate the number of unique SNs (number of players)
player_count = df_purchase_data["SN"].nunique()

# Store information in a Pandas DataFrame
df_player_count = pd.DataFrame({"Total Players" : [player_count]})

df_player_count
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
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>576</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Total)

* Number of Unique Items

* Average Purchase Price

* Total Number of Purchases

* Total Revenue



```python
# Calculate the number of unique items
unique_items = df_purchase_data["Item ID"].nunique()

# Calculate average purchase price
avg_purchase_price = df_purchase_data["Price"].mean()

# Calculate the total number of purchases
number_purchases = df_purchase_data["Purchase ID"].nunique()

# Calculate Total Revenue
total_revenue = df_purchase_data["Price"].sum()

# Store information in a Pandas DataFrame
df_purchase_analysis = pd.DataFrame({
                                    "Number of Unique Items" : [unique_items],
                                    "Average Price" : [avg_purchase_price],
                                    "Number of Purchases" : [number_purchases],
                                    "Total Revenue" : [total_revenue]
                                    })

# Formating data
df_purchase_analysis["Average Price"] = df_purchase_analysis["Average Price"].map("${:,.2f}".format)
df_purchase_analysis["Total Revenue"] = df_purchase_analysis["Total Revenue"].map("${:,.2f}".format)

df_purchase_analysis
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
      <th>Number of Unique Items</th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>183</td>
      <td>$3.05</td>
      <td>780</td>
      <td>$2,379.77</td>
    </tr>
  </tbody>
</table>
</div>



## Gender Demographics

* Percentage and Count of Male Players

* Percentage and Count of Female Players

* Percentage and Count of Other / Non-Disclosed



```python
# Create Grouped DataFrame
df_gender_demo_grp = df_purchase_data.groupby("Gender")

# Calculate Number of Player by Gender and store in a Pandas DataFrame
df_gender_number_players = pd.DataFrame(df_gender_demo_grp["SN"].nunique())

# Rename column
df_gender_number_players.columns = ["Number of Players"]

# Calculate Percentage of Players
df_gender_number_players["Percentage of Players"] = round(df_gender_number_players["Number of Players"] / player_count * 100,2)

# Sort Dataframe by Total Count
df_gender_number_players.sort_values("Number of Players", ascending = False, inplace = True)

df_gender_number_players
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
      <th>Number of Players</th>
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>484</td>
      <td>84.03</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>81</td>
      <td>14.06</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
      <td>1.91</td>
    </tr>
  </tbody>
</table>
</div>




## Purchasing Analysis (Gender)

* The below each broken by gender

    * Purchase Count
    
    * Average Purchase Price

    * Total Purchase Value
    
    * Average Purchase Total per Person by Gender
    


```python
# Calculate the total number of purchases
df_gender_number_purchases = pd.DataFrame(df_gender_demo_grp["Purchase ID"].nunique())
df_gender_number_purchases.columns = ["Purchase Count"]

# Calculate average purchase price
df_gender_avg_purchase_price = pd.DataFrame(df_gender_demo_grp["Price"].mean())
df_gender_avg_purchase_price.columns = ["Average Purchase Price"]

# Calculate Total Purchase Value
df_gender_total_revenue = pd.DataFrame(df_gender_demo_grp["Price"].sum())
df_gender_total_revenue.columns = ["Total Purchase Value"]

# Calculate Number of Player by Gender
#df_gender_number_players = pd.DataFrame(df_gender_demo_grp["SN"].nunique())
#df_gender_number_players.columns = ["Number of Players"]

# Create a summary Pandas DataFrame
df_gender_purchase_analysis = pd.merge(df_gender_number_purchases,df_gender_avg_purchase_price,on="Gender")
df_gender_purchase_analysis = pd.merge(df_gender_purchase_analysis,df_gender_total_revenue,on="Gender")
df_gender_purchase_analysis = pd.merge(df_gender_purchase_analysis,df_gender_number_players,on="Gender")

# Calculate Average Total Purchase per Person
df_gender_purchase_analysis["Avg Total Purchase per Person"] = df_gender_purchase_analysis["Total Purchase Value"] / df_gender_purchase_analysis["Number of Players"]

# Formating data
df_gender_purchase_analysis["Average Purchase Price"] = df_gender_purchase_analysis["Average Purchase Price"].map("${:,.2f}".format)
df_gender_purchase_analysis["Total Purchase Value"] = df_gender_purchase_analysis["Total Purchase Value"].map("${:,.2f}".format)
df_gender_purchase_analysis["Avg Total Purchase per Person"] = df_gender_purchase_analysis["Avg Total Purchase per Person"].map("${:,.2f}".format)

# Remove "Number of Players" and "Percentage of Players" columns
df_gender_purchase_analysis = df_gender_purchase_analysis.drop(["Number of Players","Percentage of Players"],axis=1)

df_gender_purchase_analysis
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Avg Total Purchase per Person</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>113</td>
      <td>$3.20</td>
      <td>$361.94</td>
      <td>$4.47</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>652</td>
      <td>$3.02</td>
      <td>$1,967.64</td>
      <td>$4.07</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>15</td>
      <td>$3.35</td>
      <td>$50.19</td>
      <td>$4.56</td>
    </tr>
  </tbody>
</table>
</div>



## Age Demographics

* Create bins for ages

* Categorize the existing players using the age bins.

* Calculate the numbers and percentages by age group

* Create a summary data frame to hold the results



```python
# Verify minimun and maximun ages
print(f'Minimun age: {df_purchase_data["Age"].min()}')
print(f'Maximun age: {df_purchase_data["Age"].max()}')
```

    Minimun age: 7
    Maximun age: 45



```python
# Create bins for ages
bins = [0,9,14,19,24,29,34,39,150]
labels = ['<10','10-14','15-19','20-24','25-29','30-34','35-39','40+']
df_purchase_data["Age Bins"] = pd.cut(df_purchase_data["Age"], bins = bins, labels = labels)

df_purchase_data.head()
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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>Age Bins</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
      <td>40+</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create grouped DataFrame
df_age_demo_grp = df_purchase_data.groupby('Age Bins')

# Calculate Number of Player by Age and store in a Pandas DataFrame
df_age_number_players = pd.DataFrame(df_age_demo_grp["SN"].nunique())

# Rename column
df_age_number_players.columns = ["Number of Players"]

# Calculate Percentage of Players
df_age_number_players["Percentage of Players"] = round(df_age_number_players["Number of Players"] / player_count * 100,2)

df_age_number_players
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
      <th>Number of Players</th>
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th>Age Bins</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>17</td>
      <td>2.95</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>22</td>
      <td>3.82</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>107</td>
      <td>18.58</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>258</td>
      <td>44.79</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>77</td>
      <td>13.37</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>52</td>
      <td>9.03</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>31</td>
      <td>5.38</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>12</td>
      <td>2.08</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Age)

* The below each broken into bins of 4 years (i.e. <10, 10-14, 15-19, etc.)

    * Purchase Count
    
    * Average Purchase Price
    
    * Total Purchase Value
    
    * Average Purchase Total per Person by Age Group



```python
# Calculate the total number of purchases
df_age_number_purchases = pd.DataFrame(df_age_demo_grp["Purchase ID"].nunique())
df_age_number_purchases.columns = ["Purchase Count"]

# Calculate average purchase price
df_age_avg_purchase_price = pd.DataFrame(df_age_demo_grp["Price"].mean())
df_age_avg_purchase_price.columns = ["Average Purchase Price"]

# Calculate Total Purchase Value
df_age_total_revenue = pd.DataFrame(df_age_demo_grp["Price"].sum())
df_age_total_revenue.columns = ["Total Purchase Value"]

# Create a summary Pandas DataFrame
df_age_purchase_analysis = pd.merge(df_age_number_purchases,df_age_avg_purchase_price,on="Age Bins")
df_age_purchase_analysis = pd.merge(df_age_purchase_analysis,df_age_total_revenue,on="Age Bins")
df_age_purchase_analysis = pd.merge(df_age_purchase_analysis,df_age_number_players,on="Age Bins")

# Calculate Average Total Purchase per Person
df_age_purchase_analysis["Avg Total Purchase per Person"] = df_age_purchase_analysis["Total Purchase Value"] / df_age_purchase_analysis["Number of Players"]

# Formating data
df_age_purchase_analysis["Average Purchase Price"] = df_age_purchase_analysis["Average Purchase Price"].map("${:,.2f}".format)
df_age_purchase_analysis["Total Purchase Value"] = df_age_purchase_analysis["Total Purchase Value"].map("${:,.2f}".format)
df_age_purchase_analysis["Avg Total Purchase per Person"] = df_age_purchase_analysis["Avg Total Purchase per Person"].map("${:,.2f}".format)

# Remove "Number of Players" and "Percentage of Players" columns
df_age_purchase_analysis = df_age_purchase_analysis.drop(["Number of Players","Percentage of Players"],axis=1)

df_age_purchase_analysis
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Avg Total Purchase per Person</th>
    </tr>
    <tr>
      <th>Age Bins</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>23</td>
      <td>$3.35</td>
      <td>$77.13</td>
      <td>$4.54</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>28</td>
      <td>$2.96</td>
      <td>$82.78</td>
      <td>$3.76</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>136</td>
      <td>$3.04</td>
      <td>$412.89</td>
      <td>$3.86</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>365</td>
      <td>$3.05</td>
      <td>$1,114.06</td>
      <td>$4.32</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>101</td>
      <td>$2.90</td>
      <td>$293.00</td>
      <td>$3.81</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>73</td>
      <td>$2.93</td>
      <td>$214.00</td>
      <td>$4.12</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>41</td>
      <td>$3.60</td>
      <td>$147.67</td>
      <td>$4.76</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>13</td>
      <td>$2.94</td>
      <td>$38.24</td>
      <td>$3.19</td>
    </tr>
  </tbody>
</table>
</div>



## Top Spenders

* Identify the the top 5 spenders in the game by total purchase value

    * SN
    
    * Purchase Count
    
    * Average Purchase Count
    
    * Total Purchase Value
    


```python
# Create grouped DataFrame
df_sn_purchase_grp = df_purchase_data.groupby("SN")

# Calculate the total number of purchases
df_sn_number_purchases = pd.DataFrame(df_sn_purchase_grp["Purchase ID"].nunique())
df_sn_number_purchases.columns = ["Number of Purchases"]

# Calculate average purchase price
df_sn_avg_purchase_price = pd.DataFrame(df_sn_purchase_grp["Price"].mean())
df_sn_avg_purchase_price.columns = ["Average Purchase Price"]

# Calculate total purchase value
df_sn_total_revenue = pd.DataFrame(df_sn_purchase_grp["Price"].sum())
df_sn_total_revenue.columns = ["Total Purchase Value"]

# Store information in a summary Pandas DataFrame
df_top_spenders = pd.merge(df_sn_number_purchases,df_sn_avg_purchase_price,on="SN")
df_top_spenders = pd.merge(df_top_spenders,df_sn_total_revenue,on="SN")

# Sort Data by Total Purchase Value
df_top_spenders.sort_values(by="Total Purchase Value", ascending = False, inplace = True)

# Formating data
df_top_spenders["Average Purchase Price"] = df_top_spenders["Average Purchase Price"].map("${:,.2f}".format)
df_top_spenders["Total Purchase Value"] = df_top_spenders["Total Purchase Value"].map("${:,.2f}".format)

df_top_spenders.head()
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
      <th>Number of Purchases</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Lisosia93</th>
      <td>5</td>
      <td>$3.79</td>
      <td>$18.96</td>
    </tr>
    <tr>
      <th>Idastidru52</th>
      <td>4</td>
      <td>$3.86</td>
      <td>$15.45</td>
    </tr>
    <tr>
      <th>Chamjask73</th>
      <td>3</td>
      <td>$4.61</td>
      <td>$13.83</td>
    </tr>
    <tr>
      <th>Iral74</th>
      <td>4</td>
      <td>$3.40</td>
      <td>$13.62</td>
    </tr>
    <tr>
      <th>Iskadarya95</th>
      <td>3</td>
      <td>$4.37</td>
      <td>$13.10</td>
    </tr>
  </tbody>
</table>
</div>



## Most Popular Items

* Identify the 5 most popular items by purchase count

    * Item ID
    
    * Item Name

    * Purchase Count

    * Item Price

    * Total Purchase Value



```python
# Create grouped DataFrame
df_item_purchase_grp = df_purchase_data.groupby(["Item ID","Item Name"])

# Calculate the total number of purchases
df_item_purchase = pd.DataFrame(df_item_purchase_grp["Purchase ID"].nunique())
df_item_purchase.columns = ["Number of Purchases"]

# Calculate average item price
df_item_average_price = pd.DataFrame(df_item_purchase_grp["Price"].mean())
df_item_average_price.columns = ["Average Item Price"]

# Calculate total purchase value
df_item_total_revenue = pd.DataFrame(df_item_purchase_grp["Price"].sum())
df_item_total_revenue.columns = ["Total Purchase Value"]

# Store information in a summary Pandas DataFrame
df_popular_items = pd.merge(df_item_purchase,df_item_average_price,on=["Item ID","Item Name"])
df_popular_items = pd.merge(df_popular_items,df_item_total_revenue,on=["Item ID","Item Name"])

# Sort Data by Number of Purchase
df_popular_items.sort_values(by="Number of Purchases", ascending = False, inplace = True)

# Sort Data by total purchase value and store in a new DataFrame of Most Profitable Items
df_profit_items = df_popular_items.sort_values(by="Total Purchase Value", ascending = False)

# Formating data
df_popular_items["Average Item Price"] = df_popular_items["Average Item Price"].map("${:,.2f}".format)
df_popular_items["Total Purchase Value"] = df_popular_items["Total Purchase Value"].map("${:,.2f}".format)

df_popular_items.head()
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
      <th></th>
      <th>Number of Purchases</th>
      <th>Average Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>178</th>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>12</td>
      <td>$4.23</td>
      <td>$50.76</td>
    </tr>
    <tr>
      <th>145</th>
      <th>Fiery Glass Crusader</th>
      <td>9</td>
      <td>$4.58</td>
      <td>$41.22</td>
    </tr>
    <tr>
      <th>108</th>
      <th>Extraction, Quickblade Of Trembling Hands</th>
      <td>9</td>
      <td>$3.53</td>
      <td>$31.77</td>
    </tr>
    <tr>
      <th>82</th>
      <th>Nirvana</th>
      <td>9</td>
      <td>$4.90</td>
      <td>$44.10</td>
    </tr>
    <tr>
      <th>19</th>
      <th>Pursuit, Cudgel of Necromancy</th>
      <td>8</td>
      <td>$1.02</td>
      <td>$8.16</td>
    </tr>
  </tbody>
</table>
</div>



## Most Profitable Items

* Identify the 5 most profitable items by total purchase value

    * Item ID
    
    * Item Name

    * Purchase Count

    * Item Price
    
    * Total Purchase Value



```python
# Formating data
df_profit_items["Average Item Price"] = df_profit_items["Average Item Price"].map("${:,.2f}".format)
df_profit_items["Total Purchase Value"] = df_profit_items["Total Purchase Value"].map("${:,.2f}".format)

df_profit_items.head()
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
      <th></th>
      <th>Number of Purchases</th>
      <th>Average Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>178</th>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>12</td>
      <td>$4.23</td>
      <td>$50.76</td>
    </tr>
    <tr>
      <th>82</th>
      <th>Nirvana</th>
      <td>9</td>
      <td>$4.90</td>
      <td>$44.10</td>
    </tr>
    <tr>
      <th>145</th>
      <th>Fiery Glass Crusader</th>
      <td>9</td>
      <td>$4.58</td>
      <td>$41.22</td>
    </tr>
    <tr>
      <th>92</th>
      <th>Final Critic</th>
      <td>8</td>
      <td>$4.88</td>
      <td>$39.04</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>8</td>
      <td>$4.35</td>
      <td>$34.80</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
