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

**Context:**

><i> Since 2008, guests and hosts have used Airbnb to expand on traveling possibilities and present more unique, personalized way of experiencing the world. This dataset describes the listing activity and metrics in Berlin from 2015 to 2019.</i>

**Content:**

><i> This data file includes all needed information to find out more about hosts, geographical availability, necessary metrics to make predictions and draw conclusions.</i>

**Acknowledgements:**

><i> This public dataset is part of Airbnb, and the original source can be found on the following Websites :</i>
>* AirBnB-Berlin Data : [Data 2015-2018](http://tomslee.net/category/airbnb-data)<br>
>* AirBnB-neighbourhoods geojson data : [neighbourhoods.geojson](http://insideairbnb.com/get-the-data.html)<br>
>* AirBnB-subway_entrance geojson data : Go on website [overpass-turbo.eu](http://overpass-turbo.eu/) and type : 
>```
>/*
>This is the Overpass query to get the Subway Entrance of Berlin.
>*/
>node
>  [railway=subway_entrance]
> ({{bbox}});
> out;
> ```
 ---
# Project Description

**Story :** 
> It’s March 2017. Rob, a (fictional?) KPMG employee living in Berlin, is very fond of his privacy – he lives moving in and out Airbnb’s and never shares his current address. He would like to invite a few D&A colleagues at his place for a dinner evening and decides to share the key features of his current rental: price, room_type, accommodates, bedrooms, bathrooms (see here for more information and to download historical Airbnb data). **The D&A team needs to figure out where Rob is most likely living.** The task is therefore to create a model that, given a set of room features, for a set of coordinates (latitude, longitude), **calculates a score that quantifies how likely it is that Rob is living at the given latitude-longitude.**

**Solution :**
> [About the Task] Given that Rob is Sharing the curent features of rental and we have access to his past Activity we will use a **Classification Algorithm**.
> [About the latitude-longitude] Given that Rob is Sharing the curent features of rental and we have access to his past Activity we will use a **Classification Algorithm**.
> [About the Score]<span style="color:red">cardinals</span>
**Plan :**

 > In this project, we will perform a <b>descriptive</b> and <b>exploratory</b> analysis of the data, in order to understand how the phenomena of each variable behave individually and transversely, in addition to generate <b>hypotheses</b> useful for the <b>decision-making </b> part. <b>In the predictive analytics</b> part we will present <font color = "red"><b>our task  to build a model that predicts where Rob, working at KPMG, will make his Airbnb reservation in 2017.</b></font> We will present a set of model candidate for this classification task and study their performance based on the <b>NDCG score</b> and other standard performance metric. We will look at the importance of the features in the decision making and relate the f1-score to each Berlin area with emphasis on the number of reservation per area. Finally, we will present a <b>prescriptive analysis</b> where we will do futher assumptions based on the Data in order to fine-grained our model score.    
 
> The whole analysis will follow a simple and direct structure, well detailed in all topics, aiming at the same time, to create an intuitive and simple <b> guide </b> of which steps must be followed to carry out a good analysis, to in order to understand the data involved in any study.
 
 **Results:**
 
 >**Model Performance Evaluation :** <font color = "red"><b>All Berlin</b></font> **(Standard Solution)**

| Model                  | NDCG_score_test           | Accuracy_score_test  |
| -------------          |:-------------:| -----: |
| **Random Forest**      | 0.871         | 0.789  |
| **Decision Tree**      | 0.803         | 0.801  |
| **XGboosting**         | 0.766         | 0.596  |
 

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
