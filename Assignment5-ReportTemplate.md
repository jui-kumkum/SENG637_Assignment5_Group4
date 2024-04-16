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

For C-SFRAT, our approach was to first run the entire failure data set that we were given with every model and covariate combination possible, and then determine which model is suitable for the behavior of the failure data according to some metric such as AIC (Akaike Information Criterion), BIC (Bayesian Information Criterion) and SSE (Sum of Squared Errors). [Link Text](URL)

We compared the models using Akaike's Information Criteria (AIC) and Bayesian Information Criteria (BIC), which are computed using C-SFRAT and are commonly used in model selection. The model with the best AIC should explain the greatest amount of variation using the fewest possible independent variables, the lower the AIC score, the better.

In contrast, BIC, like AIC, provides an accurate estimation of the model's performance for future data. It is preferable if the BIC score is lower.

After analyzing the Model Comparison tables from C-SFRAT, we determined that the Discrete Weibull Type 3 model, with covariate F is the best model, with AIC of 122.199 and BIC of 127.935. The second best is the Geometric Model with covariate F with AIC of 125.323 and BIC of 129.625.

After testing with the various ranges on these models, we found that using a subset of 21 of the 31 in the full set (approximately 67-70% of the full failure dataset) and setting the Covariate F as 20 efforts per interval gives best performance for the models.

One possible reason for this, is that from the 20th interval there is a huge up-climb of failures, and as such using only the subset before interval 20 will not effectively predict the failures with the models.


   ![image](https://github.com/jui-kumkum/SENG637_Assignment5_Group4/blob/main/Images/637part1.png)


# Assessment Using Reliability Demonstration Chart 

# 

# Comparison of Results

# Discussion on Similarity and Differences of the Two Techniques

# How the team work/effort was divided and managed

# 

# Difficulties encountered, challenges overcome, and lessons learned

# Comments/feedback on the lab itself
