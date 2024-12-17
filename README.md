 # Forecasting sales revenues and sales volume for an online retailer

## Business context
### Online retailer based out of UK sells unique all-occasion gifts to customers in 37+ countries, many of whom are wholesalers
### More than 90% of sales of retailer are in UK, remaining 10% are to 36+ country mainly in Europe
### Over the one year perior retailer sold 5.17M items and recorded $9.74M in total sales revenues
### Over one year retailer sold 4070 distinct SKUs, top 100 SKUs represent 30% of sales

## Business problem - supporting robust growth through high volatility
### Online retailer experienced robust growth over the past 12 months with sales volume and revenue nearly increasing by 100%
### However, daily sales volume and sales revenues experienced significant volatility over the past 12 months, with significant spikes and trough
### Such volatility in daily sales revenues with rapid sales growth makes financial planning and working capital management extremely challenging for the business, specifically for the CFO. Business faces risk of lack of available cash in a timely manner to fund the growth
### High volatility in daily sales volume with rapid growth in volume makes supply chain planning and inventory management extremely challenging. Business faces risk of stock out with lost sales as well as excess inventory.

## Solution desired by business - directionally accurate forecasting of revenues and volume
### Sales revenue forecast
#### Directionally accurate sales revenue forecast will allow CFO and Finance to develop robust financial plan using a mix revolving credit as well as short term and long term financing to fund the growth of the business.
#### Sales forecast with "possible ranges" of +/- errors will allow the Finance team to conduct scenario planning and incorporate flexibility into the financial plan

### Sales volume forecast
#### Directionally accurate sales volume forecast will allow COO and Supply Chain to develop robust demand and supply plan as well as an inventory management plan.
#### Volume forecast with "possible ranges" of +/- errors will allow the Supply Chain team to create sufficient levels of buffer stock and develop agility in the supply chain to manage the volatility in demand

## Data available to develop reveue and volume forecast
### Scope of data available
#### History - 1 year of sales data
#### Granulatity - Invoice level transactions at SKU X Customer grain with transaction time stamp
#### Data size - 541909 entries with 7 columns
#### Data fields available - SKU Identifier, Customer Identifier, Price, Quantity, Date time 

### Limitation of data
#### History is limited to one year
#### Data lacks any information of special promotions run by the retailer
#### There is no information on special "holidays" in the sales data

## Approach to developing revenue and forecasting model
### Scoped the effort to develop two forecasting models - one for sales revenue and the other for sales volume (quantity)
### Data profiling
#### After loading the data, assessed each of the columns and data types, identified any missing data (nulls)
#### About 25% of the sales transactions have a missing customer identifier (customer ID) and 0.2% of transactions have missng product description.
#### Since we are developing forecast for daily sales revenue and volume these missing data were not deemed as critical gaps
### Data preparation and feature engineering
#### For each sales transaction, calculated the revenue generated by multiplying sales quantity with price
#### Grouped all sales transactions by date and calculated sales revenue and sales volume for each date
#### Extracted day of the week, month information for each transaction
### Data visualization and findings - Sales Revenues
#### Time series view of sales revenue - variaion by date shows extreme volatility with significant spikes and troughs
#### Sales revenue trends : after experiencing an initial dip, revenue was flat and then increased signficantly towards the later part of the year 
#### Sales revenues follow a monthly pattern: revenues on a particular day is strongly correlated to revenues 30 days prior 
#### Sales revenues follow a "moderate" quarterly pattern: revenues on a particular day is moderataely correlated to revenues 90 days prior
#### Sales revenues does not follow a "weekly" pattern : revenues on a particular day in not correlated to revenues 7 days prior
### Data visualization and findings - Sales Volume
#### Time series view of sales volume - variaion by date shows extreme volatility with significant spikes and troughs
#### Sales volume trends : after experiencing an initial dip, revenue was flat and then increased signficantly towards the later part of the year 
#### Sales volumes follow a monthly pattern: volumes on a particular day is strongly correlated to revenues 30 days prior 
#### Sales volumes follow a "moderate" quarterly pattern: volumes on a particular day is moderataely correlated to revenues 90 days prior
#### Sales volumes does not follow a "weekly" pattern : volumes on a particular day in not correlated to revenues 7 days prior

### Sales revenue and volume forecasting model development - LSTM
#### We decided to use advanced Machine Language model - LSTM (Long Short Term Memory) model that has an established track record in forecasting time series data
#### We split the sales revenue and volume data into a "training" set and a "test" set
#### We used the "training" set data to train the model
##### Used the training data to have the model capture the different patterns and nuances in variation of daily revenue and volume
#### We used the test data to measure the performance of the model 
##### We would have the model predict sales revenue and volume for the dates in the test data and compare it with actual sales and volume
##### We used the RMSE (Root Mean Squared Error) metric to quantify the error in prediction and that would be the basis of comparing different models
#### We optimized the LSTM model for forecasting by tuning the models so that it yields least prediction error (RMSE) for test data set
##### We tuned the "architecture" of the model as well as how the model processes data 
##### We tried different variations of the LSTM algorithim 

## Forecasting model solution
### Sales Revenue forecast model using LSTM was able to generate forecast with accuracy of ~64% for the test period 
#### The revenue forecast model is directionally accurate and can help with financial planning 
#### However given the relatively high forecasting error rate, CFO and the Finance organization should create financial models with mechanisms to mitgate risk 
##### Need to use financial tools such as "revolving credit" and  "short term debt" to mitigate credit and liquidity risk and be able to fund growth of the business
### Sales Volume forecast model using LSTM was able to generate forecast with accuracy of ~66% for the test period 
#### The revenue forecast model is directionally accurate and can help with supply chain and inventory planning 
#### However given the relatively high forecasting error rate, COO and the Supply Chain organization should develop mechanisms to build more agility and resilience in the supply chain
##### Plan for adequate safety stock for "critical SKUs" - typically high volume and high margin SKUs
##### Collaborate and develop partnerships with key suppliers to incorporate flexibility in the Supply Plan - so that retailer can react to rapidly changing demand
### Limitation of the forecasting model
#### Forecasting model is based one year history of data and does not capture all possible patterns in the time series data
#### Model does not include information such as sales promotion, new product launch, marketing launch that may be key to explaining variation is sales revenue and volume
#### Model does not include external market information such as key holidays, interest rates, GDP growth, competitor actions that may be key to explaining variation in sales revenue and volume

## Forecasting model - recommendations
### Deploy the sales revenue forecasting model to the Finance organization within the online retailer
#### Develop processes for Finance team to review revenue forecasting model output and provide feedback
#### Incorporate revenue forecast output into annual financial planning and regular Management reports 
### Deploy the sales volume forecasting model to the Supply Chain and Planning organization within the online retailer
#### Develop processes for Supply Chain and Planning team to review volume forecasting model output and provide feedback
#### Incorporate volume forecast into annual Supply and Demand Planning as well as regular operational reporting 
### Deploy team to maintain and improve the forecasting model
#### Retrain the model every 3 - 6 months with additional data taking into account feedback from Finance and Supply Chain & Planning teams
#### Incorporate additonal internal data into the model - such as price and marketing promotions as well new product launches
#### Incorporate additional external market and macro economic data into the model - such as interest rates, GDP
#### Deploy updated and improved model every 3 to 6 months

