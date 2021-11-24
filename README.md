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
> - **<i>About the Task</i>** :  Given that Rob is sharing the curent features of rental and we have access to the past activity of all users we will use a **Classification Algorithm** to predict is current **locations.**
> - **<i>About the location</i>** :  We don't want to be too intrusive in the life of Rob, therefore we will **scale the location classification** at the 96 borought of Berlin (see [here](https://en.wikipedia.org/wiki/Boroughs_and_neighborhoods_of_Berlin))
> - **<i>About the Score</i>** : We will quantify the likelihood of Rob living in each of the 96 borought of Berlin by the predictive output score of our trained classifier. This score is the confidence score of the model on it's prediction and it can be interpreted as a probability score. We will futher tailored our solution by assuming Rob want to live close to KPMG headquarters. Indeed the trafic in Berlin is very dense. He don't want to take too much time to go to work. Therefore we proposed a finetune solution with the constraint that the Airbnb rental have to be at less than 5kilometers from KPMG headquarter. (Only : Heidestraße 58, 10557 Berlin, Germany)

**Data-Informed Decision Making :**

 > In this project, we will perform a <b>descriptive</b> and <b>exploratory</b> analysis of the data, in order to understand how the phenomena of each variable behave individually and transversely, in addition to generate <b>hypotheses</b> useful for the <b>decision-making </b> part. We will treat the missing inputs throught imputation and control the variable properties. <b>In the predictive analytics</b> part we will present our solution to the tase. Specifically, We will present a set of classifier candidate and study their performance based on the <b>NDCG score</b> and other standard performance metric. We will look at the importance of the features in the decision making and relate the f1-score to each Berlin area with emphasis on the number of reservation per area. Finally, we will present a <b>prescriptive analysis</b> where we will do futher assumptions based on the Data in order to tailord our solution to the case of Rob.    
 
> The whole analysis will follow a simple and direct structure, well detailed in all topics, aiming at the same time, to create an intuitive and simple <b> guide </b> of which steps must be followed to carry out a good analysis, to in order to understand the data involved in any study. The data consistency is paramout. We  connected it to synergetic complex models and we interpret the result. 

 **Results:**
 
 >**Model Performance Evaluation :** <font color = "red"><b>All Berlin</b></font> **(Standard Solution)**

| Model                  | NDCG_score_test           | Accuracy_score_test  |
| -------------          |:-------------:| -----: |
| **Random Forest**      | 0.871         | 0.789  |
| **Decision Tree**      | 0.803         | 0.801  |
| **XGboosting**         | 0.766         | 0.596  |

| Top 5 Area                    | Predictive Score          
| -------------                 |:-------------:|
| **Tempelhofer Vorstadt**      | 6.299         | 
| **Frankfurter Allee Süd FK**  | 5.781         |
| **Alexanderplatz**            | 4.965         | 
| **Reuterstraße**              | 4.210         | 
| **Rixdorf**                   | 3.994         | 

 
  >**Model Performance Evaluation :** <font color = "red"><b>All Berlin</b></font> **(Standard Solution)**

| Model                  | NDCG_score_test           | Accuracy_score_test  |
| -------------          |:-------------:| -----:|
| **Random Forest**      | 0.886      | 0.8099 |
| **Decision Tree**      | 0.808      | 0.6532 |
| **XGboosting**         | 0.804      | 0.7997|
 
| Top 5 Area                    | Predictive Score          
| -------------                 |:-------------:|
| **Alexanderplatz**            | 9.923         | 
| **Tempelhofer Vorstadt**      | 9.257         |
| **Brunnenstr. Süd**           | 7.353         | 
| **Prenzlauer Berg Südwest**   | 6.456         | 
| **Prenzlauer Berg Nordwest**  | 6.025         | 
 

 
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
