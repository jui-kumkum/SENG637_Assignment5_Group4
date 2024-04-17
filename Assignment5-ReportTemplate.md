**SENG 637- Dependability and Reliability of Software Systems***

**Lab. Report \#5 – Software Reliability Assessment**

| Group \#:       |   |
|-----------------|---|
| Student Names:  |   |
|                 |   |
|                 |   |
|                 |   |

# Introduction
In this assignment,  we performed integration test data using some reliability assessment tools. We will explore the use of Reliability Growth Testing (RGT) and Reliability Demonstration Chart (RDC) to assess the reliability of a software system.
Then we will compare these techniques to see what they are like and how they are different from one another.
# 

# Assessment Using Reliability Growth Testing (RGT)
For Reliability Growth Testing, after testing the tools suggested by the assignment guideline, we decided to utilize the tool C-SFRAT. The reason for choosing C-SFRAT is because the tool has a very user-friendly way to install and to compare the models with different combinations of covariates.

For C-SFRAT, our approach was to first run the entire failure data set that we were given with every model and covariate combination possible, and then determine which model is suitable for the behavior of the failure data according to some metric such as AIC (Akaike Information Criterion), BIC (Bayesian Information Criterion) and SSE (Sum of Squared Errors). See [Model Results](https://github.com/jui-kumkum/SENG637_Assignment5_Group4/blob/main/model_results.csv)

We compared the models using Akaike's Information Criteria (AIC) and Bayesian Information Criteria (BIC), which are computed using C-SFRAT and are commonly used in model selection. The model with the best AIC should explain the greatest amount of variation using the fewest possible independent variables, the lower the AIC score, the better.

In contrast, BIC, like AIC, provides an accurate estimation of the model's performance for future data. It is preferable if the BIC score is lower.

After analyzing the Model Comparison tables from C-SFRAT, we determined that the Discrete Weibull Type 3 model, with covariate F is the best model, with AIC of 122.199, BIC of 127.935 and SSE of 1087.948. The second best is the Geometric Model with covariate F with AIC of 125.323, BIC of 129.625 and SSE of 759.654.

After testing with the various ranges on these models, we found that using a subset of 21 of the 31 in the full set (approximately 67-70% of the full failure dataset) and setting the Covariate F as 20 efforts per interval gives best performance for the models.

One possible reason for this, is that from the 20th interval there is a huge up-climb of failures, and as such using only the subset before interval 20 will not effectively predict the failures with the models.

Time to Failure Plot of the two models:

   ![image](https://github.com/jui-kumkum/SENG637_Assignment5_Group4/blob/main/Images/637part1.png)

   Intensity Plot:

   ![image](https://github.com/jui-kumkum/SENG637_Assignment5_Group4/blob/main/Images/637Intensity.png)

### Calculation of Failure Rate, Mean to Failure Rate (MTTF)
From the plot and table we can measure the failure rate, Mean to Failure Rate (MTTF)  for the original failure data and the predictions (DW3 and GM) at the last interval (31).
| Dataset        | Failure Rate (F/Interval) | MTTF (intervals) |
|----------------|---------------------------|------------------|
| Raw Data       | 92/31 = 2.96              | 1/2.96 = 0.337   |
| DW3 Prediction| 91/31 = 2.94              | 1/2.94 = 0.341   |
| GM Prediction | 90/31 = 2.90              | 1/2.90 = 0.344   |

### Decision making based on given Target Failure Rate
Businesses that are concerned with their software reliability will have a target failure rate or MTTF that is considered acceptable. For example, if the business considers the acceptable failure rate to be 3 Failures/Interval, then at 31st interval this SUT would be considered acceptable as the raw data is at 2.96 failures per interval. However, using the Discrete Weibull Type 3 model, we can predict at which interval in the future the failure rate may become unacceptable.
We can see from the plot that, after interval 21 for DW3 and GM models to predict the last 10 intervals, the failure rate and MTTF are very close to the original failure data.
Here, for our raw data, failure rate is 2.96. For interval 1-8, failure rate of DW3 and GM is much lower than our raw data, for interval 10-20, failure rate is higher than the raw data,from 22-28 failure rate is lower than imported data.
### Advantages and Disadvantages of Reliability Growth Testing

#### Advantages
   + Allows the user to predict the failure behavior using a set of predefined models. Using AIC and BIC it is easy to compare which models best fit the data.
   + Through iterative testing and refinement, reliability growth testing helps to reduce the likelihood of software failures in production environments.
   + By detecting and fixing reliability issues early in the development lifecycle, reliability growth testing can help reduce the cost of software maintenance and support.

#### Disadvantages
    + Predictions are dependent on the subset of data (here range of intervals) used for the prediction. For example, if there are some distortions or outliers of data within the subset of data, the predictions might not be accurate.
    + Predictions are dependent on the model used. For example, if the model is not appropriate for the data, the predictions may not be accurate.

# Assessment Using Reliability Demonstration Chart 

# 

# Comparison of Results

# Discussion on Similarity and Differences of the Two Techniques

# How the team work/effort was divided and managed

# 

# Difficulties encountered, challenges overcome, and lessons learned

# Comments/feedback on the lab itself
