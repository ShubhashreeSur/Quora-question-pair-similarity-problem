# Quora-question-pair-similarity-problem
![](quora.jpg)

## 1. Business Problem

Quora is a place to gain and share knowledge—about anything. It’s a platform to ask questions and connect with people who contribute unique insights and quality answers. This empowers people to learn from each other and to better understand the world.

Over 100 million people visit Quora every month, so it's no surprise that many people ask similarly worded questions. Multiple questions with the same intent can cause seekers to spend more time finding the best answer to their question, and make writers feel they need to answer multiple versions of the same question. Quora values canonical questions because they provide a better experience to active seekers and writers, and offer more value to both of these groups in the long term.

**1.1 Credits: Kaggle**
Source <https://www.kaggle.com/c/quora-question-pairs>

**1.2 Problem Statement**
Given a pair of questions, we have to predict whther they have the same intent or not, i.e., whether one is a duplicate question of another?

**1.3 Business contstraints and objectives**
- The cost of a mis-classification can be very high.
- You would want a probability of a pair of questions to be duplicates so that you can choose any threshold of choice.
- No strict latency concerns.
- Interpretability is partially important.


## 2. Mapping to Machine Learning Problem

**2.1 Data Overview**
- Data will be in a file Train.csv consisting a minimum number of data fields:
    - id: Looks like a simple row ID
    - qid1: unique ID of question 1
    - qid2: unique ID of question 2
    - question1: the textual content of question 1
    - question2: the textual content of question 2
    - is_duplicate: The label that we are trying to predict - whether the two questions are duplicates of each other.

**2.2 Type of Machine learning problem**
It is a binary classification problem, for a given pair of questions we need to predict if they are duplicate or not.

**2.3 Performance metric**
- log-loss (KPI)
- confusion, precision, recall matrices


## 3. Exploratory Data Analysis and feature extraction


