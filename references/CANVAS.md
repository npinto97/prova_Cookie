# The Machine Learning Canvas

- **Designed for**: Armani
- **Designed by**: E. Molinari, E. Tanzi, N. Pinto
- **Date**: 09/10/2024
- **Iteration**: 1

## Task

**Goal**: Analyze past orders and returns to predict which products are more likely to be returned.

**Additional challenge**: Using product pictures, is there some common pattern among most returned products (e.g., same material, color, etc.)?

## Value Proposition

> Who is the end-user? What are their objectives? How will they benefit from the ML system? Mention workflow/interfaces.

The primary end-users of this system include logistics, product management, and marketing departments. Their shared objective is to reduce the frequency of product returns, which can have significant financial and operational costs. By using machine learning predictions, these teams stand to benefit through improved decision-making, particularly in terms of inventory management and product recommendations.

For logistics teams, fewer returns mean reduced reverse logistics costs, less waste, and better warehouse efficiency. For product management, understanding which products tend to be returned can lead to improved product design or better alignment between product descriptions and customer expectations. Marketing teams can also benefit by offering more accurate product recommendations that are less likely to be returned, ultimately improving customer satisfaction and retention.

## Predict

### Prediction Task

> Type of task? Entity on which predictions are made? Possible outcomes? Wait time before observation?

The central task is a binary classification problem (DA CONFERMARE IN BASE AL DATASET FORNITO) where the aim is to predict whether a product will be returned or not. The predictions will be made on individual products within customer orders. The outcomes are straightforward: either a product will be returned or it won’t. This means the machine learning system will need to analyze a variety of features linked to the product, customer, and order to determine the likelihood of a return.

AGGIUNGERE IL FATTO CHE LA CLASSIFICAZIONE PREVEDE VALORI POSITIVI PER GLI ACQUISTI E VALORI NEGATIVI (PROB -1) PER I RESI. QUINDI TUTTI I -1 SONO NELLA CLASSE DEI RESI, IL RESTO NO.

Another aspect of this task is the temporal lag involved. Returns typically occur a few days or weeks after the purchase, depending on the company's return policy. A typical waiting period of 30 days would be expected before observing whether a customer has returned an item. This time frame introduces a challenge as it delays feedback on whether the model's predictions were correct, which needs to be accounted for in model evaluation and updates.

### Decisions

> How are predictions turned
into proposed value for the end-user?
Mention parameters of the process /
application that does that.

The predictions made by the model will influence key decisions across different business areas. For instance, the logistics and inventory teams will benefit from knowing which products are more likely to be returned, as it allows them to adjust stock levels, improve return handling procedures, and reduce excess inventory costs. Similarly, the marketing and product management teams can use this information to refine product listings and descriptions. For products with a high predicted return probability, extra care can be taken to ensure accurate descriptions, provide additional product information, or recommend alternative items to customers.

The predictions could be embedded into existing decision-making systems, creating actionable insights through product alerts or automated workflows. For example, a warning flag could be triggered for products predicted to have a high return risk, prompting additional checks in the supply chain or sales process.

### Impact Simulation

> Can models be deployed?
Which test data to assess performance?
Cost/gain values for (in)correct
decisions? Fairness constraint?

Before full deployment, it will be essential to simulate the model's impact on operations. The system’s predictions can be tested using historical data, allowing the company to assess its performance in identifying products that are returned. This can be done by splitting the data into a training set for the model and a test set for validation, ensuring robust assessment of its effectiveness.

The cost of incorrect predictions will be a key factor. For example, if the model falsely predicts a high likelihood of return for a product that is not returned, this could lead to unnecessary stock adjustments or misinformed marketing strategies. On the other hand, correctly identifying high-return items will result in reduced costs and optimized inventory. Fairness constraints must also be considered; the model should not disproportionately flag certain product categories or types based on biased assumptions, ensuring that all products are treated equitably by the system.

## Learn

### Data Sources

> Where can we get (raw)
information on entities and observed
outcomes? Mention database tables,
API methods, websites to scrape, etc.

(DA RIVEDERE)
The order database will provide key information on each purchase, including customer details, product attributes, and whether a return occurred. Product images will also BE PROVIDED BY THE THE COMPANY; these can be sourced from the company’s product catalog or image repository.

(Additionally, feedback from customers—such as reviews or return reasons—can offer valuable insights into why certain products are being returned. This feedback may come from survey responses, product ratings, or direct return reasons logged in the system.)

### Data Collection

> Strategy for initial train set &
continuous update. Mention collection
rate, holdout on production entities,
cost/constraints to observe outcomes.

To train the machine learning models, a large historical dataset of product orders and returns will be required. This includes information on each product purchased, whether it was returned, and any associated metadata (such as return reasons or customer reviews). The initial dataset will consist of past order data, while the system must be updated continuously with new information as new orders and returns come in.

To ensure the model remains robust and accurate, data will need to be refreshed periodically, and holdout sets can be used to evaluate performance on products that have yet to be encountered.

### Features

> Input representations
available at prediction time,
extracted from raw data sources

(DA MODIFICA DOPO AVER OTTENUTO IL DATASET)
The input features for these models will come from a combination of structured and unstructured data. For the return prediction model, features will include information from the orders, such as product characteristics, customer demographics, price points, and past return behaviors. For the image analysis model, features will be extracted from the product images themselves, looking for visual attributes that may be associated with high return rates. Additional inputs could come from customer feedback, such as reviews or the reasons given for returning the product.

EVENTUALI COMMENTI SULLA FEATURES SELECTION

### Building Models

> How many prod models are
needed? When would we update?
Time available for this (including
featurization and analysis)?

The project will likely require two core machine learning models. The first model will focus on predicting the probability of return based on structured order data (such as product category, price, customer history, etc.). The second model will use computer vision techniques to identify common patterns among the most returned products, such as specific colors, materials, or design elements that correlate with high return rates.

These models will need to be updated regularly, perhaps on a monthly basis, to incorporate new order and return data. The training process will take time, especially for the image analysis component, as processing large sets of images requires significant computational resources.

## Monitoring

> Metrics to quantify value creation and
measure the ML system’s impact in
production (on end-users and
business)?

The PERFORMANCE of this machine learning system will be measured by its accuracy in predicting product returns and its overall impact on business operations. Key metrics to monitor include the precision and recall of the return prediction model, which will show how effectively it identifies products likely to be returned. Additionally, the reduction in overall return rates and improvements in inventory management efficiency will provide tangible evidence of the model’s value.

Over time, analyzing the visual patterns identified by the image model will help to determine whether there are common traits among returned products. Monitoring these patterns could lead to insights that influence product design and development, ultimately reducing the rate of returns at the source.
