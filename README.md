# Pizza-Delivery
Built a model for a optimization problem of orders to determine the number of chefs required in a restaurant. Using optimal balancing of loads amongst the cooks allows to quantify the output in a better way than serial orders will impact the outcomes. Trained a XGBRegressor model to predict the the number of orders and then made a decision based on the output.

1. For building the model, took multiple steps - 
Data preprocessing - Extracted time, day, month and year from the datetime. Kept day and time columns, and dropped month, and year columns as they were constant columns. Cleaned data in HOUSEHOLD_SIZE_DESC and KID_CATEGORY_DESC columns and changed it’s type to float. 
Data Analysis - There were no missing values in the dataset. The target quantity variable was skewed to the left since most people ordered an acute number of pizzas. 
Feature Engineering - Label Encoded all categorical features and found out correlation in between all the features. HOUSEHOLD_SIZE_DESC and KID_CATEGORY_DESC were highly correlated. Found out feature importance using mutual information classifier and dropped features - HOUSEHOLD_SIZE_DESC to reduce dimensions and build the model. The top 3 features that quantify the target - HH_COMP_DESC, INCOME_DE, AGE_DESC 
Model Training - Built regression models such as Linear Regression and XGB. Tuned the hyperparameters using Randomized Search. Compared the models using mean squared error and r2 score.

2. Assumptions - 
The number of orders are widely spread based on the time - There are closer to 1000 orders in the evening as compared to 100 order orders in the early morning hours. I assume that multiple shifts of cooks can be arranged according to the flux observed to optimize and increase the utilization factor. 
Dividing the number of orders in buckets - 3 different shifts could be kept with minimal variance.
Constant Service Time - Assume each cook takes the same ‘t’ amount of time to make one pizza i.e It takes n*t time to make n pizzas. 
There is optimal transfer of load taking place between the cooks. For eg, if a cook has an order of 14 pizzas whereas a cook has an order of 2 pizzas and is free afterwards, then the 14 pizzas will be load balanced with this cook to complete the order quickly.

Notation -> M/ M/ Number of cooks : FCFS/ Total_number_of_orders(<Threshold)/ Infinite queries

Mean Service rate => 10 orders per hour can be served per cook (Assumption)
Mean Arrival rate => Average(Orders) / 60 mins (Calculate for each shift)
For eg - Shift 1
Mean Arrival Rate = 78.38/60 mins
Utilization factor => 78.38/10 = 7.8 (1 cook)

Utilization factor => 78.38/10*7 = 1.12 (7 cooks)
Utilization factor => 78.38/10*8 = 0.94 (8 cooks)
Will go with 7 cooks for this shift. Can increment a cook towards the 8th hour to make sure the orders are completed with a better throughput.
Average Wait Time per customer for one pizza  => 
= Total pizzas that can be served/ Pizzas ordered(Pizzas ordered- pizzas that can be served)
= 10*7/78.38(78.38 - 10*7)
= 0.106 hrs (6.4 minutes)

Calculate for each shift, and then optimize accordingly. Using optimal balancing of loads amongst the cooks allows to quantify the output in a better way than serial orders will impact the outcomes.
