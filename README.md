<p align="center">
  <img src="Images/KPMG.png"   Width="500"></center>
</p>

**Authors:** Stanislas Furrer 

**Date :** 24.11.2021

**Requirements** : (Need to run the notebook package before doing step 3)
```
(base) conda creat --name KPMG python=3.8
(KPMG) pip install requirements.txt
(KPMG) pip install descartes
```
---
# Description of the data

AirBnB-Berlin Data : [Data 2015-2018](http://tomslee.net/category/airbnb-data)<br>
AirBnB-neighbourhoods geojson data : [neighbourhoods.geojson](http://insideairbnb.com/get-the-data.html)<br>
AirBnB-subway_entrance geojson data : Go on website [overpass-turbo.eu](http://overpass-turbo.eu/) and type : 
```
/*
This is the Overpass query to get the Subway Entrance of Berlin.
*/
node
  [railway=subway_entrance]
  ({{bbox}});
out;
```


**Context:**

><i> Since 2008, guests and hosts have used Airbnb to expand on traveling possibilities and present more unique, personalized way of experiencing the world. This dataset describes the listing activity and metrics in Berlin from 2015 to 2019.</i>

**Content:**

><i> This data file includes all needed information to find out more about hosts, geographical availability, necessary metrics to make predictions and draw conclusions.</i>

**Acknowledgements:**

><i> This public dataset is part of Airbnb, and the original source can be found on this <a href="http://tomslee.net/airbnb-data-collection-get-the-data">website</a>.</i>
 ---



# Part1. Know the facts with descriptive analytics.
---

## Part1.1 About the Data


## Part1.2 Missing Value Imputations


## Part1.3 Data Analysis

# Part2. Know what to expect with predictive analytics.
---



## Part2.1 Model Performance
## Part2.2 Model Evaluation

# Part3. Know your strategy with prescriptive analytics.
---
