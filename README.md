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
> - **<i>About the model</i>** We will favoritize tree based classifier as they handle un-balanced dataset and outliers. Specically, we will look in both standard and ensembling approach. Indeed, ensembling as the strenght to reduce the variance of the decision and generally leads to better performance. 

**Data-Informed Decision Making :**

 > In this project, we will perform a <b>descriptive</b> and <b>exploratory</b> analysis of the data, in order to understand how the phenomena of each variable behave individually and transversely, in addition to generate <b>hypotheses</b> useful for the <b>decision-making </b> part. We will treat the missing inputs throught imputation and control the variable properties. <b>In the predictive analytics</b> part we will present our solution to the tase. Specifically, We will present a set of classifier candidate and study their performance based on the <b>NDCG score</b> and other standard performance metric. We will look at the importance of the features in the decision making and relate the f1-score to each Berlin area with emphasis on the number of reservation per area. Finally, we will present a <b>prescriptive analysis</b> where we will do futher assumptions based on the Data in order to tailord our solution to the case of Rob.    
 
> The whole analysis will follow a simple and direct structure, well detailed in all topics, aiming at the same time, to create an intuitive and simple <b> guide </b> of which steps must be followed to carry out a good analysis, to in order to understand the data involved in any study. The data consistency is paramout. We  connected it to synergetic complex models and we interpret the result. 

 **Results:**
 
<p align="center">
  <img src="Images/table_KPMG.png" Width="500" ></center>
</p>

 >**Model Performance Evaluation :** All Berlin **(Standard Solution)**
<!---
| Top 3 Models             | NDCG_score_test           | Accuracy_score_test  |
| -------------          |:-------------:| -----: |
| **Random Forest**      | 0.871         | 0.789  |
| **Decision Tree**      | 0.803         | 0.801  |
| **XGboosting**         | 0.766         | 0.596  |
-->

<p align="center">
  <img src="Images/Score1.png"   Width="500"></center>
</p>
<!---
| Top 5 Areas                    | Predictive Score          
| -------------                 |:-------------:|
| **Tempelhofer Vorstadt**      | 6.299         | 
| **Frankfurter Allee Süd FK**  | 5.781         |
| **Alexanderplatz**            | 4.965         | 
| **Reuterstraße**              | 4.210         | 
| **Rixdorf**                   | 3.994         | 
-->
 
 
  >**Model Performance Evaluation :** Berlin 5 kilometer around KPMG **(Fine-Tuned Solution)**
<!---
| Top 3 Models                  | NDCG_score_test           | Accuracy_score_test  |
| -------------          |:-------------:| -----:|
| **Random Forest**      | 0.886      | 0.8099 |
| **Decision Tree**      | 0.808      | 0.6532 |
| **XGboosting**         | 0.804      | 0.7997|
-->

<p align="center">
  <img src="Images/table_KPMG2.png" Width="500" ></center>
</p>

<p align="center">
  <img src="Images/Score_5km_Fine_grained.png"   Width="500"></center>
</p> 
<!---
| Top 5 Areas                   | Predictive Score          
| -------------                 |:-------------:|
| **Alexanderplatz**            | 9.923         | 
| **Tempelhofer Vorstadt**      | 9.257         |
| **Brunnenstr. Süd**           | 7.353         | 
| **Prenzlauer Berg Südwest**   | 6.456         | 
| **Prenzlauer Berg Nordwest**  | 6.025         | 
-->

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
In this section we will present our model candidate for the recommender tasks. Specifically : 

> - We present a set of model candidat, the performance metrics and some preprocessing made. We will use as baseline model Logistic Regression and Naive Bayes. We will compare their performance with tree based algorithm as they have the nice properties to handle unbalanced dataset and outliers. We will look at a standard decision tree classifier as well as ensembling of tree with RandomForest and XGboosting. Ensembling have several advantage over regular model as they reduce the variance of the decision by some type of hierachical voting.  
> - We will then analyse the features importance in the decision making. As we might expect, the price, the number of reviews and the distances to KPMG are the most important features in the decision process. In fact, for humans, this parameters would also be our key variable for making our decision of renting an AirBnB accomodations.
> - Finally, we will inspect the evaluation metric and relate them to each area of Berlin. 

<h2 id="Preprocessing-id">A. Preprocessing</h3>

**Part1. Remove Features**
> - Some Features are not relevant for the predictive task and might even hurt or biased the model as it will increased significantly the number of parameters.

> - We will keep as features : [room_type, reviews, overall_satisfaction, accommodates, bedrooms, price, year, month, distToKPMG] and predict the [neighbourhood]. We would have keep the host_id if we would have more information about the host as it might influence the decision.

> - **IMPORTANT Note**: I tried bining bedrooms and accomodates into 6 class [1,2,3,4,5,>5]. It increase the performance of the baseline model while deacrease the performance of the tree based model. The tree based algorithm are robust to outlier where the baseline aren't. Therefore for the tree based classifier binning will remove some important information while for the baseline classifier it will reduce the impact of the outliers. Therefore **WE WON'T USE BINNING** 

**Part2. Encoding**
> - We will convert "room_type" into Categorical Data. 
> - We will make use of the function get_dummies from pandas. The dummy coding scheme is similar to the one hot encoding scheme, except in the case of dummy coding scheme, when applied on a categorical feature with m distinct labels, we get m-1 binary features. Thus each value of the categorical variable gets converted into a vector of size m-1. The extra feature is completely disregarded and thus if the category values range from {0, 1, ..., m-1} the 0th or the m-1th feature is usually represented by a vector of all zeros (0).
> - **IMPORTANT Note**:We tried to convert also "overall_satisfaction","accommodates","bedrooms","year","month" into Categorical Data and apply one hot-encoding but it hurts the performance off the tree based models. **WE WON'T USE ONE HOT ENCODING FOR THE MENTIONED VARIABLE**

To understand this, let’s get into the inner dynamics of tree-bases models. For every tree-based algorithm, there is a sub-algorithm that is used to split the dataset into two bins based on a feature and a value. The splitting algorithm considers all possible splits (based on all features and all possibles values for each feature) and finds the most optimum split based on a criterion. We will not get into details of the criterion (there are multiple ways to do this) but qualitatively speaking, the criterion helps the sub-algorithm select the split that minimizes the impurity of bins. Purity is a proxy for the number of positive or negative samples in a particular bin in a classification problem.

<p align="center">
  <img src="Images/tree_based.png"   Width="550"></center>
</p>

If a continuous variable is chosen for a split, then there would be a number of choices of values on which a tree can split and in most cases, the tree can grow in both directions. The resulting tree from a dataset containing a majority of continuous variables that would look like something in the figure to the left.

Categorical variables are naturally disadvantaged in this case and have only a few options for splitting which results in very sparse decision trees. The situation gets worse in variables that have a small number of levels and one-hot encoding falls in this category with just two levels. The trees generally tend to grow in one direction because at every split of a categorical variable there are only two values (0 or 1). The tree grows in the direction of zeroes in the dummy variables.


**Part3. Scalling**

> - We tried scalling both price and distance to KPMG with sklearn's StandardScaler() however **it hurt the performance** of three based algorithm while improving the performance of logistic regression and KNN. 
> - It is expected for logistic regression, KNN and Naive Bayes algorithm
> - Decision trees and ensemble methods do not require feature scaling to be performed as they are not sensitive to the the variance in the data. Indeed, tree based algorithm are rule based and do not compute distances. **WE WON'T USE SCALLING**


**Part4. Stratisfied klfold Cross-Validation**

>**Kfold Cross Validation**: divide the data into folds and ensure that each fold is used as a testing set at some point. It is a regularization technique that reduce the variance of the decision and the overfitting.

<p align="center">
<img src="https://miro.medium.com/proxy/1*E1e-8OmoqJaSmHxxPXcPGg.png" alt="" width="300" height="200" class="aligncenter size-full wp-image-13940" />
</p> 

>**StatifiedKfold** : Stratification is the process of rearranging the data as to ensure each fold is a good representative of the whole. For example in a binary classification problem where each class comprises 50% of the data, it is best to arrange the data such that in every fold, each class comprises around half the instances. It ensure to keep the same class distribution in each fold. In our case, we have a strong un-balanced situation, therefore this methods is essential.

**Part5. Performance Metric**

To evaluate the model performance we will use the NDCG score, f1 score and the accuracy. 

**NDCG**
>- NDCG stands for ***Normalized Discounted Cumulative Gain.***

>- To evaluate recommender systems we need to measure how relevant the results are and how good the ordering is.

>- To understand NDCG, we need to understand its predecessors: Cumulative Gain(CG) and Discounted Cumulative Gain(DCG). Also, we need to keep the following assumption in mind: *The highly relevant documents are more useful than moderately relevant documents, which are in turn more useful than irrelevant documents.*
>- The gain is  the relevance score for each item recommended. The cumulative gain at K is the sum of gains of the first K items recommended. Discounted cumulative gain weighs each relevance score based on its position. The recommendations at the top get a higher weight while the relevance of those at the bottom get a lower weight. 
<p align="center">
  <img src="Images/NDCG.png"   Width="300"></center>
</p>

> - The normalized discounted cumulative gain is the DCG with a normalization factor in the denominator. The denominator is the ideal DCG score when we recommend the most relevant items first. 
<p align="center">
  <img src="Images/NDCG_2.png"   Width="300"></center>
</p>

**F1-score** : 
> - The F1 score is defined as the harmonic mean of precision and recall.
> - As a short reminder, the harmonic mean is an alternative metric for the more common arithmetic mean. It is often useful when computing an average rate.
> - In the F1 score, we compute the average of precision and recall. They are both rates, which makes it a logical choice to use the harmonic mean. 
> - The F1-score is an excellent metric for un-balanced classes. It makes it well suits for our task. 
> The F1 score formula is shown here:

<p align="center">
  <img src="https://inside-machinelearning.com/wp-content/uploads/2021/09/F1-Score.png"  Width="200"></center>
</p>

**Accuracy** :
> - It is the most standard metric for evaluating the model performance. 
> - However, it is not well suited in our context as we have unbalanced classes.
> - We will use it as an informative metric rather than a metric to optimize. 

<p align="center">
  <img src="Images/accuracy.png"   Width="300"></center>
</p>

<h2 id="Modeling">B. Modeling</h3> 

We select tree baseline model and tree tree-based model with an increasing level of complexity. 

> **PLEASE NOTE**: We have organize our data wrangling and data processing in order to optimize the performance of the tree based algorithm. The choices that have been made are expect to hurt significantly the performance of the baseline models. Indeed, we haven't **remove the outliers** in review and price, we haven't **fix the skewedness of the price throught a logarithm scaling and a box-cox treatment**, we haven't **binned some parameters**, we haven't **one hot encode all the categorical parameters** and we haven't **Standardize any parameters**. **HOWEVER** we have carefully designed our code in order to do the mentioned process

> As expected the tree based algorithm have better performance than the baselines. Indeed, we have optimize for tree-based algorithm and for the baseline that have a lot assumptions to met. Our best model is Random Forest. 

<p align="center">
  <img src="Images/result_score.png"   Width="300"></center>
</p>

<p align="center">
  <img src="Images/result_final.png"   Width="500"></center>
</p>

> Next we analyse the importance of the features in the decision making of the tree-based classifier. 


<p align="center">
  <img src="Images/features_importance.png "   Width="800"></center>
</p>

**Obervation** : 
> * For Random Forest and Decision Tree the distance to KPMG is the most impactful parameters in the decision making. Indeed, as discused KPMG is more or less in the center of berlin. It is one of the places where there is the most AirBnB rental. Selecting KPMG as the center of interest is definitly not the best choice (we made it as a toy exemple) however it seems to be a relevant information
> * In fact the distance to KPMG leak the real position of the rental and therefore the model "short-cut" is learning process as it learn to match the relative distance to KPMG to a given neighbours.  
> * However, even if the model would perfectly fit the relation between the distance to KPMG and the area of Berlin it won't be enough as we would have to consider the radious of the distance. This might be the reason why the distance to KPMG is not the only features in the decision making.
> * The three next most important features are the price, the review and the accomodates.
> * As expected the month, year and type of room haven't so much influence as they are similarly distributed in each area. They are not relevant to make a distinction.
> * The biggest difference between the models is that XGBoosting decision is mostly impacted by the number of bedrooms and the features importance is more distributed than RandomForest and Decision Tree.


---
# 3. Prescriptive Analytics

In this section we will try to understand how we might improve our recommender system. 

> - We will examine the misclassification through the lens of the f1-score per area, emphasizing the number of occurrences of each class.
> - We will make the assumption that Rob wishes to live at most 5km far from KPMG headquarter. From this assumption, we will retrain our models to get better performance on this specific task.
> - We observe better performance of our recommender system based on all the metrics.  The main reason for this improvement comes from the better class balance induced by our assumption. Indeed, there is more listening in these areas.
> - Finally, we will delineate our conclusion and present improvements

<h2 id="result">A. Result Analysis</h3>

**F1 score Analysis**

The classes (neighbours) are highly imbalanced. Alghough the tree based algorithm are well suited to handle un-blanced dataset we might reduce this effect. In our previous analysis we show that the farrer a neighbours is from the Center of Berlin the less sample we have. In the following we plot the f1 score iin function of the distance of KPMG and vizualize for each area of Berlin. We use the f1 score as it is a well suited performance metric for unbalanced Dataset. 

<p align="center">
  <img src="Images/f1_score.png"   Width="650"></center>
</p>

**Obervation** : 
> * The f1 Score has a strong variance when the number of Airbnb Rental is low. However, the more we have data the less variance we have.  
> * The f1 Score have a Mean around 80%. 
> * The neighbours in the center are more representative of the 80% f1-score.

<h2 id="fine">B. Fine-Tuning</h3> 
We will tailord our task by assuming that Rob wish to live at most 5 kilometer far from KPMG headquarter. Hopefully, this assumption makes the classes less unbalanced as we have more rental in the center of Berlin. Algought defining KPMG distance as a features will limit the model performance, it match (under a certain precision) the center of interest of Berlin.  

<p align="center">
  <img src="Images/final_score.png"   Width="650"></center>
</p>
<p align="center">
  <img src="Images/table_KPMG2.png" Width="500" ></center>
</p>

**Obervation** : 
> * Our model have Better performance in term of the NDCG score, Accuracy and F1-score. The main cause is that the class unbalanced has be lowered by our assumption.
> * The f1 score have less variance because we have a dense sampling for each area except for **Weißensee**. According to our webseach **Weißensee** is a calm residensial area where there is not so many AirBnB.

<h2 id="Conclusion">C. Conclusion and Future work</h3> 

In this project, we have presented a data-driven approach to predict the future location of Airbnb bookings in Berlin. Specifically, we offer a probabilistic approach to quantify the area of Berlin where the users in 2017 will most probably make a reservation.

In order to solve this task, we had to proceed into data cleaning through missing input imputation and a wide range of data analyses. We then select a set of model candidates for the classification task. We analyze the performance of each model based on the NDCG score and other performance metrics (accuracy,f1-score, recall, precision). We analyze the importance of the features and present a probabilistic score for each area of Berlin. We try to understand the misclassification through the lens of the f1-score per area, emphasizing the number of occurrences of each class. Finally, we proposed a fine-grained approach that focused on a user working at KPMG Berlin who wants not to be farther than 5 kilometers from Berlin.

Our best recommender system on the fine-grained contraint (less than 5km from KPMG) obtain a **NDCG_score** = 0.887 and an **accuracy** = 80%  on the test set. The test set is all the Aibnb reservations made in 2017.

**Improvement and Future Work**

In all data Science projects, it is paramount to understand and work around the tradeoff between "the level of detail and the time requirement." Indeed, the priority is to match the company or consumer deadline with the highest output quality possible. However, it is always possible to improve the data quality, the model performance or make better visualization. This project had to be implemented in less than five days. We prioritize the overall structure with a strong emphasis on justifying our choices. 

The recommender system we built is biased by our assumption that every user is interested in being as close as possible to KPMG. This hypothesis has been made to match our scoring target per area where Rob working at KPMG might book his next flat. 

In the following, we propose a list of potential improvements. We believe the performance might be significantly improved if we include more parameters. The following might be considered as Data-centric improvement of the pipeline : 

**Data Centric :**
> * Use more data in order to have more dense sampling for each area. Add data from [insideairbnb](http://insideairbnb.com/)
> * The distances to bus or railway station might be significant in the user's choise. [Here](https://medium.com/@brendan_ward/how-to-leverage-geopandas-for-faster-snapping-of-points-to-lines-6113c94e59aa) is an implementation for computin the shortest distance to subway given a data point.
> * The Access to restaurants, shops, cafes, bars and pubs are important for Airbnb users.
> * We removed the Host Id info : However if we would have past info about the host then it would propably influence the result
> * Having access to the review comment might be usefull. We could compute a sentiment score with a BERT model finetuned for emotion classification.  
> * We could also include image quality as a feature. Shunyuan et al. 2017 [here](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2976021), have shown that Airbnb property demand changed after the acquisition of verified images (taken by Airbnb’s photographers). 


**Data Centric :**
> * Use tree pruning and Features selection to reduce the Overfitting
> * Conduct a grid search for hyper parmeter selection. **PLEASE NOTE** We have implemented the code for the grid search, however due to time constrain we haven't run it.
> * Try Deep Deural Network. Specifically, try a Multi-Layers-Perceptron with as regularization dropout and layer-normalization and as optimizer Adam. (This is my speciality. I have a lot of project where I implemented all sort of Deep Learning Architecture([here](https://github.com/stanFurrer/Multimodal-solution-for-grasp-stability-prediction), [here](https://github.com/stanFurrer/Meta-Learner-LSTM-for-Few-Shot-Learning), [here](https://github.com/stanFurrer/A-Comparison-Between-Two-Manifold-Techniques),[here](https://github.com/stanFurrer/Emotion-Analysis-On-Opensubtitle-), [here](https://github.com/stanFurrer/Robust-Multimodal-Contrastive-Learning)... ). However, I prioritize the interpretability of the project rather than optimizing the performance.)

**Lessons Learned**

1. Great opportunity to work with geographic data and to connect them to the model performance.
2. There is a tone of geographic information about transport and market for every city online and it is very intuitive to collect and work with them.


And that’s all. **This was a very fun project to work with.**

If you somehow managed to go through the whole thing and are reading this, thank you for your time! Any feedback is much appreciated.
