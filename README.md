# Credit_Risk_Analysis
This project will predict credit risk by using different over, under and combination sampling methods, along ensemble and logistic regression models on a credit card credit dataset from LendingClub, a peer-to-peer lending services company.

The performance of these different models and sampling methods will be evaluated to determine if any of these algorithms should be used for credit risk prediction tasks.

## Results

The balanced score, confusion matrix and imbalanced classification report for each of the algorithms used to assess the credit risk for the dataset is included in this section.

The confusion matrix that's generated for each method is read as follows:

```
[[  TP   FP]
 [FN TN]]
```

Where TP equals the True Positive predictions, FP equals the False Positive predictions, FN equals the False Negative predictions and TN equals the True Negative predictions. 

### Logistic Regression Models

These results were obtained using a logistic regression with the appropriate sampling algorithm. These sampling methods are used since the credit risk dataset is unbalanced and therefore requires resampling to train the model appropriately.

* Over Sampling Algorithms

![Over_Sampling_Results](/Images/Over_Sampling_Results.png)

|                     | Balanced Accuracy Score | Precision Score High Risk | Recall Score High Risk | Precision Score Low Risk | Recall Score Low Risk |
|---------------------|-------------------------|---------------------------|------------------------|--------------------------|-----------------------|
| Naive Over Sampling | 0.6373337125695099      | 0.009844                  | 0.639175               | 0.996791                 | 0.010165              |
| Smote Over Sampling | 0.6339000985853366      | 0.010165                  | 0.597938               | 0.996608                 | 0.669862              |

These two models obtained a similar balanced accuracy score, with naive over sampling having around 0.4% higher accuracy. 

The precision for high risk credit requests is low in both models, being around 1% for both models. The low risk credit requests have significantly better scores, with 99% precision for both models, and a recall above 60%.

Between these 2 over sampling methods, SMOTE Over Sampling would be the better one as seen by its F1 score, however these models are not competent for assessing high risk requests due to their low recall score. This means that part of their high risk requests would be flagged as low risk which could mean a potential loss for the credit lenders.

* Under Sampling Algorithm

![Cluster_Centroid_Under_Sampling](/Images/Under_Sampling_Results.png)

|                                  | Balanced Accuracy Score | Precision Score High Risk | Recall Score High Risk | Precision Score Low Risk | Recall Score Low Risk |
|----------------------------------|-------------------------|---------------------------|------------------------|--------------------------|-----------------------|| Cluster Centroids Under Sampling | 0.524682188835512       | 0.006142                  | 0.597938               | 0.994976                 | 0.451426              |

The cluster centroid under sampling has an accuracy score of 52.4%. The high risk credit request precision has a value of 0.6% and a recall of 59%. The low risk credit request precision has a value of 99.4% and a recall of 45%. 

The F1 score for this method for high risk requests is really low, with a value of 1.2%. Therefore this model can't be used for credit risk predictions because of its low recall in both high risk and low risk requests.

* SMOTEENN Sampling Algorithm

![SMOTEENN_Combined_Sampling](/Images/SMOTEEN_Results.png)

|                                  | Balanced Accuracy Score | Precision Score High Risk | Recall Score High Risk | Precision Score Low Risk | Recall Score Low Risk |
|----------------------------------|-------------------------|---------------------------|------------------------|--------------------------|-----------------------|| SMOTEENN Combination Sampling    | 0.6787636579257549      | 0.010211                  | 0.793814               | 0.997930                 | 0.563713              |

The SMOTEENN method has a balanced accuracy of 67.8%. Among the logistic regression models, SMOTEEN has the highest Recall and F1 score for high risk credit which means that this model is more likely to identify the actual high risk requests correctly. 

While its low risk precision is 99%, meaning that whenever the model flags a request as low risk means that its 99% likely to be true, the low recall score of 56% means that almost half of the low risk requests would not be classified as such.

### Ensemble Models

![Ensemble_Model_Results](/Images/Ensemble_Results.png)

| Balanced Accuracy Score | Precision Score High Risk | Recall Score High Risk | Precision Score Low Risk | Recall Score Low Risk |
|-----------------------------------|-------------------------|---------------------------|------------------------|--------------------------|-----------------------|| Balanced Random Forest Classifier | 0.7957716773246495      | 0.046132                  | 0.670103               | 0.997974                 | 0.921440              |
| Easy Ensemble AdaBoost Classifier | 0.9179891724857726      | 0.090336                  | 0.886598               | 0.999323                 | 0.949380              |

The tree classifiers performed the best in this task. The Balanced Random Forest Classifier has an accuracy score of 79.5% while the Easy Ensemble Classifier reached a score of 91.7%. 

The low risk prediction of both models gave excellent results; Balanced Random Forest Classifier precision score is 99.7% and its recall score is 92.14%, Easy Ensemble Classifier precision score is 99.9% and its recall is 94.93%. The high recall score of these models means that at least 90% of all low risk requests will be correctly labelled as such.

Regarding the high risk prediction, the Balanced Random Forest Classifier scored 4.6% precision and 67% recall, while the Easy Ensemble Classifier scored 9% precision and 88.6% recall. These results mean that the Easy Ensemble Classifier will do a much better job at detecting the high risk requests, with only 11.4% of these slipping by as false negatives.

## Summary 


|                                   | Balanced Accuracy Score | Precision Score High Risk | Recall Score High Risk | Precision Score Low Risk | Recall Score Low Risk |
|-----------------------------------|-------------------------|---------------------------|------------------------|--------------------------|-----------------------|
| Naive Over Sampling               | 0.6373337125695099      | 0.009844                  | 0.639175               | 0.996791                 | 0.010165              |
| Smote Over Sampling               | 0.6339000985853366      | 0.010165                  | 0.597938               | 0.996608                 | 0.669862              |
| Cluster Centroids Under Sampling  | 0.524682188835512       | 0.006142                  | 0.597938               | 0.994976                 | 0.451426              |
| SMOTEENN Combination Sampling     | 0.6787636579257549      | 0.010211                  | 0.793814               | 0.997930                 | 0.563713              |
| Balanced Random Forest Classifier | 0.7957716773246495      | 0.046132                  | 0.670103               | 0.997974                 | 0.921440              |
| Easy Ensemble AdaBoost Classifier | 0.9179891724857726      | 0.090336                  | 0.886598               | 0.999323                 | 0.949380              |

In the high risk credit requests, it's much better to have a high recall than a high precision. The reason for this is that a high risk request could translate into monetary loss or complications for the credit lender, a high recall % would ensure that less high risk requests are erroneously classified as low risk. In this aspect, the Easy Ensemble AdaBoost Classifier outperforms the rest of the algorithsm with its 88.6% recall. 

All of the used algorithms result in a low precision score, with Easy Ensemble being the highest at 9%, this implies that out of the requests labelled as high risk, only 9% of these would be correctly labelled as such. In a credit lending bussiness this means that potential customers might be left out. However the Easy Ensemble Classifier has really high scores with the low risk predictions.

Considering the results of all the used models, the Easy Ensemble AdaBoost Classifier would be the most appropriate solution for the credit risk prediction business given how it doesnt allow most of the high risk requests to be labelled as low risk, which means a safer option for a credit lender.