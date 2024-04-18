**SENG 637- Dependability and Reliability of Software Systems***

**Lab. Report \#5 – Software Reliability Assessment**

| Group: 4      |
|-----------------|
| Student 1 Arpita Chowdhury                |   
| Student 2 Fadila Abdulai Hamid             |   
| Student 3 Kumkum Akter             |   
| Student 4 Niloofar Sharifisadr              |
| Student 5 Pratishtha Pratishtha |  

# Introduction
In this assignment,  we performed integration test data using some reliability assessment tools. We will explore the use of reliability assessment tools:
1. Reliability Growth Testing (RGT)
2. Reliability Demonstration Chart (RDC) to assess the reliability of a software system.

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

The RDC serves as a pivotal tool in the evaluation process for product development and quality control. Its purpose is to provide clear, visual guidance for decision-making about a product by integrating risk factors into its analysis. This is particularly beneficial when information about failures alone does not offer a complete assessment.

The RDC is structured around three primary risk considerations:

+ Discrimination Ratio (γ): This parameter reflects the inherent product risk. A lower γ value suggests a higher acceptance level for the product, indicating a lower inherent risk. Conversely, a higher γ increases the product's rejectability, signaling higher risk.
+ Customer's Risk (β): This risk level represents the probability that a product will fail after being deemed acceptable. The standard value is 0.1, implying a 10% tolerance for customer risk. Decreasing β expands the 'continue' decision zone, implying a more lenient threshold for product acceptance from the customer's standpoint.
+ Developer's Risk (α): This is the probability of rejecting a product that would have met the reliability criteria. Also typically set at 0.1, a reduction in α broadens the 'continue' region, allowing for more flexibility in development and testing phases before making a final decision.
These factors contribute to the shape and boundaries of the RDC, thus influencing the decision to accept, reject, or continue testing a product. The 'continue' region is particularly crucial as it defines the threshold where additional data or testing is warranted to make a more informed decision.

To effectively apply the RDC, it's necessary to establish a target MTTF or failure rate (λ_F) that is appropriate for the product's intended use. This target is informed by the specific requirements and tolerances of the product's application. The failure data set, as gathered in the initial part of the assessment, provides the empirical basis for applying the RDC in a real-world context.

# 

Before representing the failure data, modifications were required. The initial data presented the count of failures within each interval, as opposed to the duration between successive failures. 

To convert the failure count data into intervals between failures, we used the following approach:

1. Divide each time interval \( T \) by the failure count \( FC \) to get the time between each individual failure.
2. Calculate the cumulative time by adding each individual time between failures from the start to the current point.

For the given dataset where the time intervals \( T \) are consistent (each \( T \) represents a new interval, for instance, T=1 for the first interval, T=2 for the second, and so on), and the failure count \( FC \) represents the number of failures in each interval, the calculations would proceed as follows for each row:

- The first entry at \( T=1 \) with \( FC=2 \) would mean that there is 0.5 time units between each failure, and the first failure is at 0.5 and the second at 1.0 cumulatively.
- For \( T=2 \) with \( FC=11 \), each failure is spaced at \(1/11) time units apart within this interval.
- and so on for the rest of the rows.

<img src="media/Azure_snap.png" width="800" />

<img src="media/Azure_snap.png" width="800" />

<img src="media/Azure_snap.png" width="800" />

<img src="media/Azure_snap.png" width="800" />
  
### Advantages of RDC:

+ RDC provides a clear visual representation of where a product stands in terms of reliability, which aids in decision-making processes.
+ It incorporates risk considerations directly into the evaluation, helping to balance and understand the implications of customer risk (β), developer's risk (α), and the discrimination ratio (γ).
+ RDC can be adjusted to different confidence levels and risk tolerances, making it adaptable to various industries and applications.
+ By using quantitative data, the RDC facilitates an objective assessment of reliability, reducing the subjective judgment that can often influence such decisions.
+ The RDC clearly delineates the actions to be taken, whether to accept, reject, or continue testing, based on the plotted failure points.
+ It allows for comparison against industry standards or regulatory requirements by setting target MTTF or failure rates.

### Disadvantages of RDC:

+ The effectiveness of RDC is heavily dependent on the quality and completeness of failure data, which can sometimes be difficult to ascertain.
+ Understanding and correctly interpreting an RDC can be complex, especially for those without statistical or reliability engineering backgrounds.
+ RDC focuses on failures and does not account for other aspects of product quality, such as features, user experience, or performance under varied conditions.
+ The use of RDC involves assumptions (e.g., failure events are evenly distributed within intervals) that may oversimplify the real-world complexities of product reliability.
+ The pursuit of higher reliability levels as suggested by RDC might incur significant costs in product development and testing, impacting the overall budget and potentially the price of the product.
+ RDC provides a snapshot based on current data and may not dynamically account for changes in use or environmental conditions over time.

# Comparison of Results


For the comparative metric, we use the minimum Mean Time To Failure (MTTF_min) of 0.046 that is established in the Reliability Demonstration Chart.
According to the RDC's determination, an MTTF_min of 0.046 is the threshold. From the Reliability Growth perspective, the SUT's MTTF stands at 0.337, rendering it acceptable by exceeding the benchmark. The RDC, on the other hand, provides a straightforward visual indicator for when the failures shift into regions that signify rejection or acceptance, showcasing the RDC's efficacy in evaluating whether the SUT meets the criteria.
In summary, the two methodologies serve distinct purposes: Reliability Growth Testing is adept at forecasting failure patterns over time, while the Reliability Demonstration Chart excels at guiding the decision on the conclusion of testing, factoring in various levels of risk.

# Discussion on Similarity and Differences of the Two Techniques

### Similarities:

+ Both RGT and RDC are centered around evaluating the reliability of a system. They are used to assess whether a system is likely to perform without failure for a desired period under specified conditions.
+ Both methodologies require failure data as a fundamental input for analysis. They analyze this data to make inferences about the reliability performance of the system.
+ RGT and RDC aid decision-makers in determining the adequacy of a system's reliability. They help in deciding whether the system can be released, needs further improvement, or requires additional testing.
+ RGT and RDC both employ statistical methods to assess and demonstrate reliability, utilizing calculations based on failure times and rates to quantify the reliability of the system.

### Differences:

+ RGT is primarily used to track and improve reliability over time through iterative testing and fixing of identified failures, focusing on the growth aspect. In contrast, RDC is used to make a binary decision on whether a system's reliability meets specified thresholds at a given point in time, typically towards the end of the testing phase.
+ RGT often requires more detailed failure data over multiple iterations and is generally more data-intensive, as it seeks to monitor reliability trends. RDC can typically provide insights with less data, as it is concerned with demonstrating reliability at a specific instance rather than its growth.
+ RGT involves ongoing testing and is a dynamic process that aims to show improvement in reliability over time. On the other hand, RDC is a static assessment that does not inherently account for changes in reliability over time but rather assesses it at a snapshot in time.
+ While both methods may use graphical representations, the RDC specifically employs a chart to visually demonstrate whether the system meets the set reliability criteria, often comparing against confidence bounds. RGT graphs are more focused on showing the trend or trajectory of reliability improvement over the course of the testing period.
  
# How the team work/effort was divided and managed

| Tester    | Section |
|-----------------|---------------|
| Arpita Chowdhury| Assessment using RGT            |   
|  Kumkum Akter |  Assessment using RGT           |   
|  Niloofar Sharifisadr | Assessment using RDC     |
| Pratishtha Pratishtha | Assessment using RDC|
| Fadila Abdulai Hamid |              |


# Difficulties encountered, challenges overcome, and lessons learned
1. We faced some difficulties in getting the right tool for our project. Our group first decided to test SRTAT-SRE-tool, but we could not import the failure data using SRTAT. Moreover, there wasn't any documentation available for the tool either, on how to use it and what input formats it supports. After that we moved to C-SFRAT.
2. We had problems with visualizing with SRTAT software. The visualization only showed the first few rows of the data and did not include all the points. We couldn't fix this issue so we moved to using RDC for the rest of the part 2. 

# Comments/feedback on the lab itself
1. We learned about how to assess the failre rate using some reliability assessment tools. 
2. One of the recommended software SRTAT-SRE-tool for RGT is very hard to use. There is no documentation available for it as well.
3. There was very little documentation on the failure dataset.
