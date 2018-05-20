
PYBER


```python
# Modules
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
```


```python
city_csv = "city_data.csv"
ride_csv = "ride_data.csv"
```


```python
city_df = pd.read_csv(city_csv)
ride_df = pd.read_csv(ride_csv)
```


```python
city_df.head()
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
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nguyenbury</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East Douglas</td>
      <td>12</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>West Dawnfurt</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rodriguezburgh</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
ride_df.head()
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
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wiseborough</td>
      <td>2016-01-21 17:35:29</td>
      <td>44.18</td>
      <td>3645042422587</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spencertown</td>
      <td>2016-07-31 14:53:22</td>
      <td>6.87</td>
      <td>2242596575892</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nguyenbury</td>
      <td>2016-07-09 04:42:44</td>
      <td>6.28</td>
      <td>1543057793673</td>
    </tr>
  </tbody>
</table>
</div>




```python
ride_city_df = pd.merge(ride_df,city_df,on="city")
ride_city_df.head()
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
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Sarabury</td>
      <td>2016-07-23 07:42:44</td>
      <td>21.76</td>
      <td>7546681945283</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sarabury</td>
      <td>2016-04-02 04:32:25</td>
      <td>38.03</td>
      <td>4932495851866</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Sarabury</td>
      <td>2016-06-23 05:03:41</td>
      <td>26.82</td>
      <td>6711035373406</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Sarabury</td>
      <td>2016-09-30 12:48:34</td>
      <td>30.30</td>
      <td>6388737278232</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
#group by city 
group_city_df = ride_city_df.groupby(['city','type'])

#average fare per city
average_fare = group_city_df["fare"].mean()

#total number of rides per city
total_rides_city = group_city_df["city"].count()

#total number of drivers per city
total_driver_city= group_city_df["driver_count"].mean()

#create new dataframe by city
city_summary = pd.DataFrame({"Average Fare":average_fare,
                             "Total Number of Ride":total_rides_city,
                            "Total Number of Drivers":total_driver_city})

city_summary.head()
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
      <th>Average Fare</th>
      <th>Total Number of Drivers</th>
      <th>Total Number of Ride</th>
    </tr>
    <tr>
      <th>city</th>
      <th>type</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <th>Urban</th>
      <td>23.928710</td>
      <td>21</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <th>Urban</th>
      <td>20.609615</td>
      <td>67</td>
      <td>26</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <th>Suburban</th>
      <td>37.315556</td>
      <td>16</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <th>Urban</th>
      <td>23.625000</td>
      <td>21</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <th>Urban</th>
      <td>21.981579</td>
      <td>49</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Bubble Plot of Ride Sharing Data

x_axis = city_summary['Total Number of Ride']
y_axis = city_summary['Average Fare']
s = city_summary['Total Number of Drivers']
labels = ["Urban","Suburban","Rural"]
colors = ["gold","lightskyblue","lightcoral"]


plt.scatter(x_axis,y_axis,marker = "o",facecolors = ["gold","lightskyblue","lightcoral"],label=labels, edgecolors ="black",s=s)

plt.xlim(0,40)
plt.ylim (15,45)
plt.title ("Pyber Ride Sharing Data (2016)")
plt.xlabel ("Total Number of Rides (Per City)")
plt.ylabel ("Average Fare ($)")
plt.legend (loc = "upper right")

plt.show()
```


![png](output_8_0.png)



```python
# % of Total Fares by City Type Pie Chart
#group by city type 
group_city_df = ride_city_df.groupby(['type'])

# % of Total Fares by City Type
total_fare = ride_city_df["fare"].sum()
percent_fare = (group_city_df ["fare"].sum()/total_fare)

#create new dataframe by city type
fares_df = pd.DataFrame({"Percent of Fare":percent_fare})

type_list = fares_df.keys()
fares_pie = fares_df.plot(kind="pie",y=type_list,
                          title="% of Total Fares by City Type",
                         legend=False,colors=["gold","lightskyblue","lightcoral"],
                          shadow =True, startangle=140,autopct="%1.1f%%",
                         explode=[0,0,.1])
fares_pie.axis('equal')
plt.show()
```


![png](output_9_0.png)



```python
# % of Total Rides by City Type Pie Chart

# % of Total Rides by City Type
total_rides = ride_city_df["ride_id"].count()
percent_rides = group_city_df ["ride_id"].count()/total_rides

#create new dataframe by city type
rides_df = pd.DataFrame({"Percent of Rides":percent_rides})

type_list = rides_df.keys()
rides_pie = rides_df.plot(kind="pie",y=type_list,
                          title="% of Total Rides by City Type",
                         legend=False,colors=["gold","lightskyblue","lightcoral"],
                          shadow =True, startangle=140,autopct="%1.1f%%",
                         explode=[0,0,.1])
rides_pie.axis('equal')
plt.show()
```


![png](output_10_0.png)



```python
# % of Total Drivers by City Type Pie Chart

# % of Total Drivers by City Type
total_drivers = city_df["driver_count"].sum()
percent_drivers = group_city_df ["driver_count"].sum()/total_drivers

#create new dataframe by city type
drivers_df = pd.DataFrame({"Percent of Rides":percent_drivers})

type_list = drivers_df.keys()
drivers_pie = drivers_df.plot(kind="pie",y=type_list,
                          title="% of Total Drivers by City Type",
                         legend=False,colors=["gold","lightskyblue","lightcoral"],
                          shadow =True, startangle=140,autopct="%1.1f%%",
                         explode=[0,0,.1])
drivers_pie.axis('equal')
plt.show()
```


![png](output_11_0.png)


# Observations
1. Urban areas have the majority of drivers, riders and fares.
2. Suburban and rural areas have higher fares compared to the low amount of drivers. May be due to distance which would cause fares to rise.
3. Suburban and rural areas also have higher demand of riders relative to the percent of drivers. Public transportion could influence rider demand.
