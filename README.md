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
 
 >**Model Performance Evaluation :** All Berlin **(Standard Solution)**

| Top 3 Models             | NDCG_score_test           | Accuracy_score_test  |
| -------------          |:-------------:| -----: |
| **Random Forest**      | 0.871         | 0.789  |
| **Decision Tree**      | 0.803         | 0.801  |
| **XGboosting**         | 0.766         | 0.596  |

<p align="center">
  <img src="Images/Score1.png"   Width="500"></center>
</p>

| Top 5 Areas                    | Predictive Score          
| -------------                 |:-------------:|
| **Tempelhofer Vorstadt**      | 6.299         | 
| **Frankfurter Allee Süd FK**  | 5.781         |
| **Alexanderplatz**            | 4.965         | 
| **Reuterstraße**              | 4.210         | 
| **Rixdorf**                   | 3.994         | 

 
 
  >**Model Performance Evaluation :** Berlin 5 kilometer around KPMG **(Fine-Tuned Solution)**

| Top 3 Models                  | NDCG_score_test           | Accuracy_score_test  |
| -------------          |:-------------:| -----:|
| **Random Forest**      | 0.886      | 0.8099 |
| **Decision Tree**      | 0.808      | 0.6532 |
| **XGboosting**         | 0.804      | 0.7997|
 
<p align="center">
  <img src="Images/Score_5km_Fine_grained.png"   Width="500"></center>
</p> 
 
| Top 5 Areas                   | Predictive Score          
| -------------                 |:-------------:|
| **Alexanderplatz**            | 9.923         | 
| **Tempelhofer Vorstadt**      | 9.257         |
| **Brunnenstr. Süd**           | 7.353         | 
| **Prenzlauer Berg Südwest**   | 6.456         | 
| **Prenzlauer Berg Nordwest**  | 6.025         | 

 ---
# Outline

**1. Descriptive Analytics**<br>
A. [Variable types](#type)<br>
B. [Missing Values Analysis and Treatment](#missing)<br>
C. [Frequency Distribution](#freq)<br>
D. [Outliers Analysis](#Outlier)<br>
E. [Bivariate Analysis](#bivariate)<br>
F. [Multivariate Analysis](#multivariate)<br>
G. [Geographic Analysis](#geo)<br>
H. [Normality](#Normality)<br>

**3. Predictive Analytics**<br>
A. [Preprocessing](#Preprocessing)<br>
B. [Modeling](#Modeling)<br>

**4. Prescriptive Analytics**<br>
A. [Result Analysis](#result)<br>
B. [Fine-Tuning](#fine)<br>
C. [Conclusion and Future work](#Conclusion)<br>

---
# 1. Descriptive Analytics

---
# 2. Predictive Analytics
<h2 id="Preprocessing-id">A. Preprocessing</h3>
<h2 id="Modeling">B. Modeling</h3> 

---
# 3. Prescriptive Analytics

In this section we will try to understand how we might improve our recommender system. 

> - We will examine the misclassification through the lens of the f1-score per area, emphasizing the number of occurrences of each class.
> - We will make the assumption that Rob wishes to live at most 5km far from KPMG headquarter. From this assumption, we will retraine our model to get better performance on this more specific task.
> - We observe better performance of our recommender system based on all the metrics.  The main reason for this improvement comes from the better class balance induced by our assumption. Indeed, there is more listening in these areas.
> - Finally, we will delineate our conclusion and present improvements

<h2 id="result">A. Result Analysis</h3>


<h2 id="fine">B. Fine-Tuning</h3> 



<h2 id="Conclusion">C. Conclusion and Future work</h3> 

In this project, we have presented a data-driven approach to predict the future location of Airbnb bookings in Berlin. Specifically, we offer a probabilistic approach to quantify the area of Berlin where the users in 2017 will most probably make a reservation.

In order to solve this task, we had to proceed into data cleaning through missing input imputation and a wide range of data analyses. We then select a set of model candidates for the classification task. We analyze the performance of each model based on the NDCG score and other performance metrics (accuracy,f1-score, recall, precision). We analyze the importance of the features and present a probabilistic score for each area of Berlin. We try to understand the misclassification through the lens of the f1-score per area, emphasizing the number of occurrences of each class. Finally, we proposed a fine-grained approach that focused on a user working at KPMG Berlin who wants not to be farther than 5 kilometers from Berlin.

Our best recommender system on the fine-grained contraint (less than 5km from KPMG) obtain a **NDCG_score** = 0.887 and an **accuracy** = 80%  on the test set. The test set is all the Aibnb reservations made in 2017.

**Improvement and Future Work**

In all data Science projects, it is paramount to understand and work around the tradeoff between "the level of detail and the time requirement." Indeed, the priority is to match the company or consumer deadline with the highest output quality possible. However, it is always possible to improve the data quality, the model performance or make better visualization. This project had to be implemented in less than five days. We prioritize the overall structure with a strong emphasis on justifying our choices. 

The recommender system we built is biased by our assumption that every user is interested in being as close as possible to KPMG. This hypothesis has been made to match our scoring target per area where Rob working at KPMG might book his next flat. 

In the following, we propose a list of potential improvements. We believe the performance might be significantly improved if we include more parameters. The following might be considered as Data-centric improvement of the pipeline : 

**Data Centric :**
> * The distances to bus or railway station might be significant in the user's choise. [Here](https://medium.com/@brendan_ward/how-to-leverage-geopandas-for-faster-snapping-of-points-to-lines-6113c94e59aa) is an implementation for computin the shortest distance to subway given a data point.
> * The Access to restaurants, shops, cafes, bars and pubs are important for Airbnb users.
> * We removed the Host Id info : However if we would have past info about the host then it would propably influence the result
> * Having access to the review comment might be usefull. We could compute a sentiment score with a BERT model finetuned for emotion classification.  
> * We could also include image quality as a feature. Shunyuan et al. 2017 [here](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2976021), have shown that Airbnb property demand changed after the acquisition of verified images (taken by Airbnb’s photographers). 

**Lessons Learned**

1. Great opportunity to work with geographic data and to connect them to the model performance.
2. There is a tone of geographic information about transport and market for every city online and it is very intuitive to collect and work with them.


And that’s all. **This was a very fun project to work with.**

If you somehow managed to go through the whole thing and are reading this, thank you for your time! Any feedback is much appreciated.
