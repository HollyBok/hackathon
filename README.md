# Exploration and Classification of the 2017 European Red List of Endangered Species

Author: Holly Bok 

## Problem Statement

The goal of this project is to explore the relationships between species and endangerment. The data used for this project is from the European Red List, which gives each species a ranking for level of endangerment, such as 'extinct' or 'least concern'. The list also includes information about the taxonomy of each species and other notes on population spread, dietary habits, etc. This project aims to accurately classify a species' level of endangerment using taxonomic groupings and basic environmental information. 

Three classification models are created - a Random Forest Classifier, a Decision Tree Classifier, and a Logistic Regression. The performance of the models is evaluated based on the accuracy scores (the proportion of predictions that the model gets correct) as compared to the baseline (the accuracy score of predicting that all species belong to the largest category - in this case a score of 0.52). The model with the highest accuracy is used to make predictions for the level of endangerment of each species. These predictions are evaluated and explored and the benefits / drawbacks of the model are discussed. 

## Data

The data is gathered from the 'European Red List 2017' Kaggle dataset by user Amal Jayaranga seen here: https://www.kaggle.com/amal19/european-red-list-2017 . A copy is available in the 'datasets' folder of this repository. The European Red List is "a review of the status of European species according to IUCN Regional Red Listing guidelines. It identifies those species that are threatened with extinction at the European level (Pan-Europe and the European Union) so that appropriate conservation action can be taken to improve their status." (source: https://ec.europa.eu/environment/nature/conservation/species/redlist/). The 2017 Red List dataset includes information extracted from November 2009 - November 2017 and includes 11670 individual species.

Species in this dataset are described by their taxonomic information and ranked by their level of endangerment. Taxonomic information for each species includes all levels from Species to Kingdom. Endangerment is ranked from "least concern" to "extinct" and is in the following hierarchy:


**Most Endangered to Least Endangered**

Extinct

Extinct in the Wild

Regionally Extinct

Critically Endangered Possibly Extinct

Critically Endangered

Endangered

Vulnerable

Near Threatened

Least Concern

Also included: Data Deficient and Not Evaluated



## Modeling

The models that are used for this project are a Random Forest Classifier, a Decision Tree, and a Logistic Regression. These classification models are compared for performance using their accuracy scores (the percentage of total predictions made that are correct). GridSearch is used to identify the best hyperparameters for each model where appropriate.

The model with the highest overall accuracy for the training and testing sets was the Random Forest Classifier (training = 0.93 ; testing = 0.64). However, while the scores for this model are highest overall they also suggest high variance. The testing score is much, much lower than the training score (a 0.29 differential in accuracy) suggesting the model is overfit to the testing data. The Logistic Regression model has the same problem (training = 0.82 ; testing = 0.63) although the differential is not as large. The Decision Tree model had the most stable scores between training and testing (training = 0.68 ; testing = 0.64) suggesting that this model has the best bias/variance tradeoff of all three. As the testing scores among the three models are basically equal and the Decision Tree has the lowest variance, this model is used to make predictions and aid in analysis. 


## Analysis / Conclusions / Future Recommendations

Overall, the majority of species are predicted to be data deficient or of least concern with very few species predicted (from most species predicted for a category to least) as vulnerable, endangered, near threatened, critically endangered, or extinct. This distribution is almost identical to the true distribution of species endangerment. 

One of the best predictors features overall is whether or not a species is endemic. If a species is endemic that means that the species is specific to the area in which its domain resides. Endemic species are found in only one geographic location. In the case of the European Red List, endemic species are species that are found in Europe and only Europe (such as the Spanish Imperial Eagle or Scottish Wildcat). The proportion of endemic and non-endemic species in the database is about even (47% endemic and 53% non endemic), but the endemic species are much more common in the more vulnerable / endangered categories. It makes sense that we see the endemic category as a good predictor because endemic species are naturally more vulnerable to endangerment because they have isolated populations by definition. Species that are not isolated to one area are likely more adaptable, have larger populations, and will not be as affected by local environmental, resource, or habitat fluctuations. This is very well reflected by the model as 100% of species predicted to be extinct in the wild are endemic and only 30% of species predicted as "least concern" are endemic.

While endemicy is the best predictor of extinction, certain taxonomic features provide valuable insight as well. Freshwater fish (especially salmon) and mollusks are the most vulnerable to high levels of endangerment. We see freshwater fish in almost all of the highly endangered categories. Avian / bird taxa are also commonly seen in the highly endangered and extinct categories. It makes sense that we would see birds and freshwater fish in extremely endangered categories as these kinds of species are very fragile and minute changes in ecosystems can have massive detrimental effects on their populations size and health. Fresh water fish in particular are experiencing global population declines due to overuse of resources and destruction of fresh water habitats.

In comparison, marine (salt water) fish taxa are more common in the less vulnerable categories. Of the species predicted as "least concern", the largest taxonomic class present is Insecta. Insects are not present in the critically endangered / more vulnerable categories. This suggests that insects are the most resilient to population destruction and ecosystem change. This is not surprising as insects are infamously indestructible and tend to maintain persistent population sizes even under extreme conditions.

The majority of the "population trend" data shows that the trend of population sizes for most species are unknown (over 50%) or stable (25%), so "increasing" and "decreasing" population trends are not that present or predictive. I would imagine that if we knew all of the unknown trends that "population trend" would be a much better predictor of the level of endangerment of a species. In general a lot of the species are categorized as "data deficient", likely due to unknown information such as population trends.

For further research, I would like to utilize the same modeling systems with changes to the data set. I found that it was sometimes difficult to nail down specific relationships between taxa and endangerment because of the sheer size of some taxonomic groups. For example, while it is interesting to know that a large portion of the species that are extinct in the wild are in the Kingdom Plantae - a Kingdom is such a *massive* classification that this does not provide as much specific or applicable information as the less broad classifications. It would be interesting to see how the results of this model change when the larger taxonomic classifications are not used as features and only smaller, more specific taxonomic groupings are included. Additionally, I would be interested in finding a way to quantify some of the qualitative features in the Rest List data set. This would be a very difficult task as much of the information in the original dataset is input as full sentences and paragraphs. Considering there are over 11,000 species included in the dataset, it would be impossible for one person to accurately convert all of that information to meaningful quantitative data and / or ranking systems. However, if there were to be a reliable and efficient way to gather more quantitative data I believe a lot of the other features present in the original data set would prove to be very useful predictors of endangerment. 
