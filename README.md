# Quora-question-pair-similarity-problem
![](quora.jpg)

## 1. Business Problem

Quora is a place to gain and share knowledge—about anything. It’s a platform to ask questions and connect with people who contribute unique insights and quality answers. This empowers people to learn from each other and to better understand the world.

Over 100 million people visit Quora every month, so it's no surprise that many people ask similarly worded questions. Multiple questions with the same intent can cause seekers to spend more time finding the best answer to their question, and make writers feel they need to answer multiple versions of the same question. Quora values canonical questions because they provide a better experience to active seekers and writers, and offer more value to both of these groups in the long term.

#### 1.1 Credits: Kaggle 
Source: <https://www.kaggle.com/c/quora-question-pairs>

#### 1.2 Problem Statement 
Given a pair of questions, we have to predict whther they have the same intent or not, i.e., whether one is a duplicate question of another?

#### 1.3 Business contstraints and objectives 
- The cost of a mis-classification can be very high.
- You would want a probability of a pair of questions to be duplicates so that you can choose any threshold of choice.
- No strict latency concerns.
- Interpretability is partially important.


## 2. Mapping to Machine Learning Problem

#### 2.1 Data Overview
- Data will be in a file Train.csv consisting a minimum number of data fields:
    - id: Looks like a simple row ID
    - qid1: unique ID of question 1
    - qid2: unique ID of question 2
    - question1: the textual content of question 1
    - question2: the textual content of question 2
    - is_duplicate: The label that we are trying to predict - whether the two questions are duplicates of each other.

#### 2.2 Type of Machine learning problem
It is a binary classification problem, for a given pair of questions we need to predict if they are duplicate or not.

#### 2.3 Performance metric
- log-loss (KPI)
- confusion, precision, recall matrices


## 3. Exploratory Data Analysis and feature extraction

#### 3.1 EDA
Did some basic analysis and visualizations to answer a few questions like:
- what is the distribution of the class labels? (using bar plots)
- What is the number of unique questions?
- Occurances of each question (using histograms)
- Are there any frequently occuring words for different classes? (using word clouds)
- To check if some of the features are useful or not (using violin plots, pair plots, pdfs)

#### 3.2 Basic feature extraction
We contructed some basic features like:
- freq_qid1 = Frequency of qid1's
- freq_qid2 = Frequency of qid2's
- q1len = Length of q1
- q2len = Length of q2
- q1_n_words = Number of words in Question 1
- q2_n_words = Number of words in Question 2
- word_Common = (Number of common unique words in Question 1 and Question 2)
- word_Total =(Total num of words in Question 1 + Total num of words in Question 2)
- word_share = (word_common)/(word_Total)
- freq_q1+freq_q2 = sum total of frequency of qid1 and qid2
- freq_q1-freq_q2 = absolute difference of frequency of qid1 and qid2

#### 3.3 Advanced Feature extraction (NLP and fuzzy features)
Some terms:
- Token: You get a token by splitting sentence a space
- Stop_Word : stop words as per NLTK.
- Word : A token that is not a stop_word

Features:
- cwc_min : Ratio of common_word_count to min lenghth of word count of Q1 and Q2</n>
cwc_min = common_word_count / (min(len(q1_words), len(q2_words))

- cwc_max : Ratio of common_word_count to max lenghth of word count of Q1 and Q2
cwc_max = common_word_count / (max(len(q1_words), len(q2_words))

- csc_min : Ratio of common_stop_count to min lenghth of stop count of Q1 and Q2
csc_min = common_stop_count / (min(len(q1_stops), len(q2_stops))

- csc_max : Ratio of common_stop_count to max lenghth of stop count of Q1 and Q2
csc_max = common_stop_count / (max(len(q1_stops), len(q2_stops))

- ctc_min : Ratio of common_token_count to min lenghth of token count of Q1 and Q2
ctc_min = common_token_count / (min(len(q1_tokens), len(q2_tokens))

- ctc_max : Ratio of common_token_count to max lenghth of token count of Q1 and Q2
ctc_max = common_token_count / (max(len(q1_tokens), len(q2_tokens))

- last_word_eq : Check if First word of both questions is equal or not
last_word_eq = int(q1_tokens[-1] == q2_tokens[-1])

- first_word_eq : Check if First word of both questions is equal or not
first_word_eq = int(q1_tokens[0] == q2_tokens[0])

- abs_len_diff : Abs. length difference
abs_len_diff = abs(len(q1_tokens) - len(q2_tokens))

- mean_len : Average Token Length of both Questions
mean_len = (len(q1_tokens) + len(q2_tokens))/2

- fuzz_ratio : <https://github.com/seatgeek/fuzzywuzzy#usage http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/>

- fuzz_partial_ratio : <https://github.com/seatgeek/fuzzywuzzy#usage http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/>

- token_sort_ratio : <https://github.com/seatgeek/fuzzywuzzy#usage http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/>

- token_set_ratio : <https://github.com/seatgeek/fuzzywuzzy#usage http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/>

- longest_substr_ratio : Ratio of length longest common substring to min lenghth of token count of Q1 and Q2
longest_substr_ratio = len(longest common substring) / (min(len(q1_tokens), len(q2_tokens))

