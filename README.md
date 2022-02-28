# eCommerce_Fraud_Detection
E-commerce websites often transact huge amounts of money. And whenever a huge amount of money is moved, there is a high risk of users performing fraudulent activities, e.g. using stolen credit cards, doing money laundry, etc. Company XYZ is an e-commerce site that sells electronic products. The objective of this project is to create a fraud-detection algorithm to flag a transition as fraudulent or not based on a single transaction.

## Data set
There are 2 tables:
1. Fraud_Data.csv: it contains information about each user and the transaction info such as user_id, signup_time, purchase_time, purchase_value, device_id, source, browser, sex, age, ip_address, class
2. IpAddress_to_Country.csv: it contains each country's lower_bound_ip_address and upper_bound_ip_address

## Some specific points/tasks to discuss
### 1. For each user, determine their country based on the numeric IP address
This is done using a conditional .loc function.
### 2. Some data explortary observations:
1.Nearly all of the fraudulent transactions were made immediately after signup, which is very different from legitimate trasactions.
![image](https://user-images.githubusercontent.com/52012182/156066919-931955f9-c78e-4d27-a2f5-dc44bc24c4ec.png)

2.We have unbalanced classes - only 10% of the transactions are fraudulent; if we do not correct for this, the model will tend to select the majority class (“0” for notfraudulent)

![image](https://user-images.githubusercontent.com/52012182/156067052-bd5e9eb7-7bb4-48cc-9f56-fb170609a772.png)

3.While the United States has the highest count of total fraudulent transactions, Uzbekistan has the highest fraud transaction ratio.
![image](https://user-images.githubusercontent.com/52012182/156067522-efa7f010-1328-451c-b376-fa74eb75cf93.png)
![image](https://user-images.githubusercontent.com/52012182/156067554-2b1f4301-f36b-47c8-808a-b2cfc1d1272d.png)

## Modeling
Predict fradulent trasactions using 3 different machine learning models with Synthetic Minority Over-sampling Technique: Logestic Regression, Random Forest, AdaBoost. Tuned the parameters by GridSearch Cross Validation.
![image](https://user-images.githubusercontent.com/52012182/156069164-3756440b-bc5c-4032-ab08-709f76ae3332.png)

## Evaluation on Fraud Characteristics
Based on the analysis of machine learning results, some fraud characteristics were found:
1. the larger number of device were shared, the higher rate of fraud

  ![image](https://user-images.githubusercontent.com/52012182/156070695-103cda4c-1d09-496c-83f9-b299d85b17ed.png)

2. more than half of fraud happened 1s after signed up

  ![image](https://user-images.githubusercontent.com/52012182/156070983-17b4ecf9-e25d-4cef-9727-c142f10f815e.png)

## Real-time Prediction
Generate class probabilities from the prediction results as shown in below, if the probability level is between 1 and 3 then pass, elif between 4-7 then need further manual identification, else between 8 and 9 then decline the trasaction.

![image](https://user-images.githubusercontent.com/52012182/156071848-2f9bdbb2-f075-4745-bef3-7f1437a479ee.png)


