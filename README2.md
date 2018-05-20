
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
urban = ride_city_df[ride_city_df["type"]== "Urban"]
suburban = ride_city_df[ride_city_df["type"]== "Suburban"]
rural = ride_city_df[ride_city_df["type"]== "Rural"]

```


```python
urban_ride_count = urban.groupby("city").count()["ride_id"]
urban_average_fare = urban.groupby("city").mean()["fare"]
urban_driver_count = urban.groupby("city").mean()["driver_count"]

suburban_ride_count = suburban.groupby("city").count()["ride_id"]
suburban_average_fare = suburban.groupby("city").mean()["fare"]
suburban_driver_count = suburban.groupby("city").mean()["driver_count"]

rural_ride_count = rural.groupby("city").count()["ride_id"]
rural_average_fare = rural.groupby("city").mean()["fare"]
rural_driver_count = rural.groupby("city").mean()["driver_count"]


plt.scatter(urban_ride_count,urban_average_fare,s=5*urban_driver_count,
            marker = "o",facecolors="lightcoral",edgecolors ="black",label ="Urban")
plt.scatter(suburban_ride_count,suburban_average_fare,s=5*suburban_driver_count,
            marker = "o",facecolors="lightskyblue",edgecolors ="black",label ="Suburban")
plt.scatter(rural_ride_count,rural_average_fare,s=5*rural_driver_count,
            marker = "o",facecolors="gold",edgecolors ="black",label ="Rural")

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
1. Rural areas have higher fares than suburban and urban areas even though rural has lower number of rides
2. Urban areas dominate the number of drivers, riders and fares.
3. Even though rural and suburban areas have 1% and 13% of drivers, respectively, they have about 6% to 30% of fares and rides. They drivers in rural and suburban areas have a higher rate of fares and rides compared to their urban counterparts.
