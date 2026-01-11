# Stock Market Real-Time Data Analytics Pipeline on AWS



### Step 2: 
Attach the following policies for ```sh Lambda_Kinesis_DynamoDB_Role```
```sh
AmazonKinesisFullAccess
AmazonDynamoDBFullAccess
AWSLambdaBasicExecutionRole
AmazonS3FullAccess
```

### Step 3: 
Run this SQL query to test:
```sql
SELECT * FROM stock_data_table LIMIT 10;
```

Find Top 5 Stocks with the Highest Price Change
```sql
SELECT symbol, price, previous_close,
       (price - previous_close) AS price_change
FROM stock_data_table
ORDER BY price_change DESC
LIMIT 5;
```

Get Average Trading Volume Per Stock
```sql
SELECT symbol, AVG(volume) AS avg_volume
FROM stock_data_table
GROUP BY symbol;
```

Find Anomalous Stocks (Price Change > 5%)
```sql
SELECT symbol, price, previous_close,
       ROUND(((price - previous_close) / previous_close) * 100, 2) AS change_percent
FROM stock_data_table
WHERE ABS(((price - previous_close) / previous_close) * 100) > 5;
```

Step 4:
Attach the following policies for ```sh StockTrendLambdaRole```
```sh
AmazonDynamoDBFullAccess
AmazonSNSFullAccess
AWSLambdaBasicExecutionRole
```
