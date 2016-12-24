# Titanic-Survival-Prediction
The popular Titanic dataset ia available and as part of practice competition in [Kaggle](https://www.kaggle.com/c/titanic). 
For the full HTML page output, please click this **[link](http://htmlpreview.github.io/?https://github.com/netsatsawat/Titanic-Survival-Prediction/blob/master/Titanic_survival_prediction.html)**.
## Data Exploratory

In the Rmd script, I will use *library(Amelia)* for quick visualization on the missing data, and another code to actual get the number of the missing data points. There are also some other library which I used (apart from ggplot2) to visualize the relationship of the feature to survival binary output.

![Heatmap](https://github.com/netsatsawat/Titanic-Survival-Prediction/blob/master/Image/Missing%20Data%20Heatmap.jpeg)

**Sample code and output**
```
library(vcd)
mosaicplot(training.data$pclass ~ training.data$survived, 
           main="Passenger Fate by Traveling Class", shade=FALSE, 
           color=TRUE, xlab="Passenger class", ylab="Survived")
```

![Mosaicplot 1](https://github.com/netsatsawat/Titanic-Survival-Prediction/blob/master/Image/Passenger%20Fate%20by%20class.jpeg)

## Prediction

Finally we will use *randomForest* library to make the prediction as well as *party::cforest* and compare the result.

![RF](https://github.com/netsatsawat/Titanic-Survival-Prediction/blob/master/Image/RF.jpeg)

![ctree](https://github.com/netsatsawat/Titanic-Survival-Prediction/blob/master/Image/ctree.jpeg)

Outcome from randomForest library
```
confusionMatrix(test.batch.rf.pred, test.batch$survived)
```

```
## Confusion Matrix and Statistics
## 
##           Reference
## Prediction  0  1
##          0 96 18
##          1 13 50
##                                         
##                Accuracy : 0.825         
##                  95% CI : (0.761, 0.878)
##     No Information Rate : 0.616         
##     P-Value [Acc > NIR] : 1.3e-09       
##                                         
##                   Kappa : 0.625         
##  Mcnemar's Test P-Value : 0.472         
##                                         
##             Sensitivity : 0.881         
##             Specificity : 0.735         
##          Pos Pred Value : 0.842         
##          Neg Pred Value : 0.794         
##              Prevalence : 0.616         
##          Detection Rate : 0.542         
##    Detection Prevalence : 0.644         
##       Balanced Accuracy : 0.808         
##                                         
##        'Positive' Class : 0             
## 
```
```
Outcome from party library (unbiased forest)
```
```
confusionMatrix(test.batch.party.pred, test.batch$survived)
## Confusion Matrix and Statistics
## 
##           Reference
## Prediction   0   1
##          0 102  16
##          1   7  52
##                                         
##                Accuracy : 0.87          
##                  95% CI : (0.811, 0.916)
##     No Information Rate : 0.616         
##     P-Value [Acc > NIR] : 6e-14         
##                                         
##                   Kappa : 0.718         
##  Mcnemar's Test P-Value : 0.0953        
##                                         
##             Sensitivity : 0.936         
##             Specificity : 0.765         
##          Pos Pred Value : 0.864         
##          Neg Pred Value : 0.881         
##              Prevalence : 0.616         
##          Detection Rate : 0.576         
##    Detection Prevalence : 0.667         
##       Balanced Accuracy : 0.850         
##                                         
##        'Positive' Class : 0             
## 
```
