# Featuretools: automated feature engineering

[![Circle CI](https://circleci.com/gh/Featuretools/featuretools.svg?maxAge=2592000&style=shield)](https://circleci.com/gh/Featuretools/featuretools)
[![Coverage Status](https://codecov.io/gh/Featuretools/featuretools/branch/master/graph/badge.svg)](https://codecov.io/gh/Featuretools/featuretools)
[![PyPI version](https://badge.fury.io/py/featuretools.svg?maxAge=2592000)](https://badge.fury.io/py/featuretools)

[Featuretools](https://www.featuretools.com) is a python library for automated feature engineering. See the [documentation](https://docs.featuretools.com) for more information.

*"One of the holy grails of machine learning is to automate more and more of the feature engineering process."* 
― Pedro Domingos, [A Few Useful Things to Know about Machine Learning](https://homes.cs.washington.edu/~pedrod/papers/cacm12.pdf)

## Installation
Install with pip

	pip install featuretools

## Example
Below is an example of using Deep Feature Synthesis (DFS) to perform automated feature engineering. In this example, we apply DFS to a multi-table dataset consisting of timestamped customer transactions.

```python
>> import featuretools as ft
>> es = ft.demo.load_mock_customer(return_entityset=True)
>> es
```
```
Entityset: transactions
  Entities:
    customers (shape = [5, 3])
    sessions (shape = [35, 4])
    products (shape = [5, 2])
    transactions (shape = [500, 5])
  Relationships:
    transactions.product_id -> products.product_id
    transactions.session_id -> sessions.session_id
    sessions.customer_id -> customers.customer_id
```

Featuretools can automatically create a single table of features for any "target entity"
```python
>> feature_matrix, features_defs = ft.dfs(entityset=es, target_entity="customers")
>> feature_matrix.head(5)
```

```
            zip_code  COUNT(transactions)  COUNT(sessions)  SUM(transactions.amount) MODE(sessions.device)  MIN(transactions.amount)  MAX(transactions.amount)  YEAR(join_date)  SKEW(transactions.amount)  DAY(join_date)                   ...                     SUM(sessions.MIN(transactions.amount))  MAX(sessions.SKEW(transactions.amount))  MAX(sessions.MIN(transactions.amount))  SUM(sessions.MEAN(transactions.amount))  STD(sessions.SUM(transactions.amount))  STD(sessions.MEAN(transactions.amount))  SKEW(sessions.MEAN(transactions.amount))  STD(sessions.MAX(transactions.amount))  NUM_UNIQUE(sessions.DAY(session_start))  MIN(sessions.SKEW(transactions.amount))
customer_id                                                                                                                                                                                                                                  ...                                                                                                                                                                                                                                                                                                                                                                                                                                          
1              60091                  131               10                  10236.77               desktop                      5.60                    149.95             2008                   0.070041               1                   ...                                                     169.77                                 0.610052                                   41.95                               791.976505                              175.939423                                 9.299023                                 -0.377150                                5.857976                                        1                                -0.395358
2              02139                  122                8                   9118.81                mobile                      5.81                    149.15             2008                   0.028647              20                   ...                                                     114.85                                 0.492531                                   42.96                               596.243506                              230.333502                                10.925037                                  0.962350                                7.420480                                        1                                -0.470007
3              02139                   78                5                   5758.24               desktop                      6.78                    147.73             2008                   0.070814              10                   ...                                                      64.98                                 0.645728                                   21.77                               369.770121                              471.048551                                 9.819148                                 -0.244976                               12.537259                                        1                                -0.630425
4              60091                  111                8                   8205.28               desktop                      5.73                    149.56             2008                   0.087986              30                   ...                                                      83.53                                 0.516262                                   17.27                               584.673126                              322.883448                                13.065436                                 -0.548969                               12.738488                                        1                                -0.497169
5              02139                   58                4                   4571.37                tablet                      5.91                    148.17             2008                   0.085883              19                   ...                                                      73.09                                 0.830112                                   27.46                               313.448942                              198.522508                                 8.950528                                  0.098885                                5.599228                                        1                                -0.396571

[5 rows x 69 columns]
```
We now have a feature vector for each customer that can be used for machine learning. See the [documentation on Deep Feature Synthesis](https://docs.featuretools.com/automated_feature_engineering/afe.html) for more examples.

## Support

For installation or usage questions, please reach out on [Gitter](https://gitter.im/featuretools/featuretools). 

## Feature Labs


<a href="https://www.featurelabs.com/">
    <img src="https://www.featurelabs.com/img/logo.png" alt="Featuretools" />
</a>


Featuretools was created by the developers at [Feature Labs](https://www.featurelabs.com/). If building impactful data science pipelines is important to you or your business, please [get in touch](https://www.featurelabs.com/contact.html).

