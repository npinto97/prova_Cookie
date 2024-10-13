# The Machine Learning Canvas

- **Designed for**: Armani
- **Designed by**: E. Molinari, N. Pinto, E. Tanzi
- **Date**: 09/10/2024
- **Iteration**: 1

## Task

**Goal**: Analyze past orders and returns to predict which products are more likely to be returned.

**Additional challenge**: Using product pictures, is there some common pattern among most returned products (e.g., same material, color, etc.)?

## Value Proposition

> Who is the end-user? What are their objectives? How will they benefit from the ML system? Mention workflow/interfaces.

The primary end-users of this system include logistics, product management, and marketing departments. Their shared objective is to reduce the frequency of product returns, which can have significant financial and operational costs. By using machine learning predictions, these teams stand to benefit through improved decision-making, particularly in terms of inventory management and product recommendations.

For logistics teams, fewer returns mean reduced reverse logistics costs, less waste, and better warehouse efficiency. For product management, understanding which products tend to be returned can lead to improved product design or better alignment between product descriptions and customer expectations. Marketing teams can also benefit by offering more accurate product recommendations that are less likely to be returned, ultimately improving customer satisfaction and retention.

Moreover, the system could be enhanced by implementing a better management approach for users with a high return rate. For example, accounts with consistently elevated return activity could face certain limitations, such as restricted access to future purchases or the need for additional verification before placing orders.
## Predict

### Prediction Task

> Type of task? Entity on which predictions are made? Possible outcomes? Wait time before observation?

The central task is a **multi-output prediction problem** where the objective is to predict both whether a product will be returned and the time frame in which the return is likely to occur. The model will operate at the individual product level within customer orders, as each product may have a different return probability and return timing. The outcomes will therefore include two components: whether a product will be returned and an estimated return window (e.g., within 7 days, within 30 days). To achieve this, the system will need to analyze a diverse set of features related to the product, customer behavior, and order details, capturing both return likelihood and temporal patterns. This approach provides a more comprehensive prediction, addressing not only the risk of return but also when the return might happen.

Another aspect of this task is the temporal lag involved. Returns typically occur a few days or weeks after the purchase, depending on the company's return policy. A 90-day window is typically required to observe whether a customer has returned an item. This delay introduces a challenge, as it postpones feedback on the accuracy of the model's predictions. However, the model is updated monthly, using data collected within the previous 90 days. This ensures that the system continually incorporates the most recent return patterns, though it still requires careful consideration of this lag when evaluating the model's performance and effectiveness in reducing returns.

### Decisions

> How are predictions turned
into proposed value for the end-user?
Mention parameters of the process /
application that does that.

The predictions made by the model will now provide more detailed insights that can influence key decisions across different business areas. For instance, the logistics and inventory teams will not only benefit from knowing **which** products are likely to be returned, but also from understanding **when** these returns are expected to occur. This will allow for more precise adjustments to stock levels, improved planning for return handling procedures, and better inventory management to reduce excess stock at critical times. Similarly, marketing and product management teams can leverage both the likelihood and timing of returns to refine product listings and descriptions. For products with a high predicted return probability, especially those expected to be returned within a short time frame, extra care can be taken to ensure accurate descriptions, provide additional product information, or recommend alternative items to customers, thus potentially reducing returns.

These predictions can be embedded into existing decision-making systems to generate actionable insights through product alerts or automated workflows. For example, a warning flag could be triggered not only for products at high risk of return but also for those predicted to be returned within a specific time window, prompting timely checks in the supply chain or adjustments in sales and marketing strategies. This allows for more dynamic and proactive management of product returns.

### Impact Simulation

> Can models be deployed?
Which test data to assess performance?
Cost/gain values for (in)correct
decisions? Fairness constraint?

Before full deployment, it will be essential to simulate the model's impact on operations. The system’s predictions can be tested using historical data to assess its performance in predicting both which products are likely to be returned and when those returns are expected to occur. This will involve splitting the data into a training set for the model and a test set for validation, ensuring robust assessment of the model's effectiveness in handling both return likelihood and timing predictions.

The cost of incorrect predictions will be a critical factor. For instance, if the model inaccurately predicts a high return likelihood or provides an incorrect return time frame, it could lead to unnecessary stock adjustments, misinformed marketing strategies, or inefficient handling of inventory. Conversely, correctly identifying both the likelihood and the time frame of returns will lead to more precise inventory management, reduced return-related costs, and better customer service. Fairness constraints must also be considered to ensure the model does not disproportionately flag certain product categories or characteristics due to biased assumptions, ensuring equitable treatment across all products.

The predictions could be integrated into existing decision-making systems, generating actionable insights through product alerts or automated workflows. For example, a warning flag could be triggered for products with a high predicted return probability or an imminent return time frame, prompting additional quality checks, adjustments in marketing approaches, or tailored customer communications to mitigate returns and manage expectations.

### Making Prediction
> When do we make real-time/
 batch pred.? Time available for this +
 featurization + post-processing? Compute target?

The ML system will operate on an event-driven basis, generating predictions whenever new customer orders are placed and relevant data is uploaded to the company's database. This approach allows for timely analysis of individual products within each order, predicting both the likelihood of return and the estimated return window based on the most recent information. Given the nature of the ordering process and the expected return time frames, real-time inference is not required. Instead, predictions will be made shortly after the data becomes available, ensuring that the latest order details are considered for inventory management and marketing adjustments.

Since product images also need to be processed to detect patterns related to return risk, the computational workload may be substantial. To accommodate these demands, the system will require robust cloud or server resources capable of handling the combined tasks of predictive modeling and image analysis, with computations typically performed in a batch-like manner soon after new orders are recorded.

## Learn

### Data Sources

> Where can we get (raw)
information on entities and observed
outcomes? Mention database tables,
API methods, websites to scrape, etc.

The order database will provide key information on each purchase, including customer details, product attributes, and whether a return occurred. Product images will also be provided by the company; these can be sourced from the company’s product catalog or image repository.

Additionally, feedback from customers - such as reviews or return reasons - can offer valuable insights into why certain products are being returned.

### Data Collection

> Strategy for initial train set &
continuous update. Mention collection
rate, holdout on production entities,
cost/constraints to observe outcomes.

To train the machine learning models, a large historical dataset of product orders and returns will be required. This includes information on each product purchased, whether it was returned, and any associated metadata, such as return reasons. The initial dataset will consist of past order data, while the system must be updated continuously with new information as new orders and returns come in.

To ensure the model remains robust and accurate, data will need to be refreshed periodically, and holdout sets can be used to evaluate performance on products that have yet to be encountered.

### Features

> Input representations
available at prediction time,
extracted from raw data sources

The input features for these models will come from a combination of structured and unstructured data. For the return prediction model, features will include information from the orders, such as product characteristics, customer demographics, price points, and past return behaviors. For the image analysis model, features will be extracted from the product images themselves, looking for visual attributes that may be associated with high return rates. Additional inputs could come from customer feedback, such as reviews or the reasons given for returning the product.

### Building Models

> How many prod models are
needed? When would we update?
Time available for this (including
featurization and analysis)?

The project will likely require a single machine learning model or a combination of models capable of handling both tasks. The first component of the model will predict the probability of a product being returned based on structured order data (such as product category, price, customer history, etc.). The second component will predict the expected time frame for the return, estimating when the return is most likely to occur (e.g., within 7 days or 30 days). Additionally, computer vision techniques will be used to identify common patterns among the most returned products, such as specific colors, materials, or design elements that may correlate with both the likelihood of return and the timing of the return.

This unified model will need regular updates, perhaps on a monthly basis, to integrate new order and return data. The training process will require significant computational resources, particularly for the image analysis component, as large sets of product images need to be processed and analyzed for relevant visual patterns.

## Monitoring

> Metrics to quantify value creation and
measure the ML system’s impact in
production (on end-users and
business)?

The performance of this machine learning system will be measured by its accuracy in predicting product returns and its overall impact on business operations. Key metrics to monitor include the precision and recall of the return prediction model, which will show how effectively it identifies products likely to be returned. Additionally, the system's capability to recognize users with a high return rate will serve as a qualitative metric, helping to mitigate potential fraud by blocking or limiting the activities of fraudulent users. 

Moreover, the model will assess the importance of the return by defining a risk factor proportional to the cost of the returned product. This will enable the system to recommend less expensive products to users who frequently return high-cost items, thus aligning product recommendations with the likelihood of returns. The reduction in overall return rates and improvements in inventory management efficiency will provide tangible evidence of the model’s value.

Over time, analyzing the visual patterns identified by the image model will help to determine whether there are common traits among returned products. Monitoring these patterns could lead to insights that influence product design and development, ultimately reducing the rate of returns at the source. 