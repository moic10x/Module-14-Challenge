# Machine Learning Trading Algo

This repo contains a notebook that starts with a basic algo bot with a strategy that enters a long position every time there is a period of positive return and enters a short postion every time there is a period of negative return. We then used machine learning to train a model to predict whether an emerging market stock will go up or down. 

## Libraries

The python notebook uses the following libraries Pandas and SkLearn. 

## Findings

The initial trading algorithm actually had a negative return as is evidenced in the below chart.

![OG_Strategy]("/Starter_Code/original_strategy.png")

If someone invested in this strategy in 2015 they would have 60% of their money in 2021.

Then we trained a support vector machine clssifier ("SVM") model to create a new strategy that would signal a short position when it predicted that returns would go down and signal a long position when it predicted returns would go up. We trained this model on the first three months of data that we had and tested on the rest of the dataset through 2021. The features of the dataset used to train the model were simple moving averages ("SMAs") of the closing prices of the emerging market stock. One was an SMA fast whihc had a rolling window of 4 periods and the other was an SMA slow which had a window of 100 periods. The result of the strategy built with the SVM model is highlighted below:

![SVM_Strategy]("/Starter_Code/svm_strategy_v_actual.png")

The strategy built by the SVM model tracked the returns of the ememerging market stock, but it started to diverge and become more profitable in 2018 until the 2020 COVID related shock forces it back to tracking the benchmark. 

We expanded the training dataset for the SVM model from 3 months to 9 months to see how performance would vary.

![SVM_long_train]("/Starter_Code/svm_strategy_longer_train_v_actual.png")

We also trained the model with shorter SMA slow window of 50 periods (maintained tranining dataset to the first three months of avaialble data as the original).

![SVM_sma_slow_50]("/Starter_Code/svm_strategy_short_50_sma_train_v_actual.png")

It seems that increasing the size of the training dataset is not helping improve performance of the trading strategy. Though the model trained with the 50 period SMA slow feature produced returns superior to actual they were not as good as those of the original model. Further tuning of the original model is required to achieve improved performance.

We also created a signaling strategy using a different model, the Decision Tree Classifier. We kept the features the same as what we used in the SVM a 4 and 100 period moving average, but used a much larger traning set of 36 months.

![Decision_Tree]("/Starter_Code/tree_strategy_v_actual.png")

