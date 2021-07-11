
### Submission by:
1. Sachin Dangayach (sachin.dangayach@gmail.com)

# Objective

## 1. Implement the following metrics (either on separate models or same, your choice):
- Recall, Precision, and F1 Score
- BLEU
- Perplexity (explain whether you are using bigram, trigram, or something else, what does your PPL score represent?)
- BERTScore

## Solution:

| Metrics | Colab Link     |
| :-------- | :------- |
| `Recall, Precision, and F1 Score` | ***[Recall, Precision, and F1 Score](https://colab.research.google.com/drive/162bjGKjd0yoEaOMHuSMI5lnJgEp0F19t?usp=sharing)*** |
| `BLEU` | ***[BLEU](https://colab.research.google.com/drive/1hgLps6L0yQ6_rs8Hjmv5-UFg-vkPpmsA?usp=sharing)*** |
| `Perplexity` | ***[Perplexity](https://colab.research.google.com/drive/14IT1IX5NlpX69rG9RG0kVSE2CoLaRRe_?usp=sharing)*** |
| `BERTScore` | ***[BERTScore](https://colab.research.google.com/drive/13NtGgFdGg9qcYVPtxJTAGRAfgjhC0nsb?usp=sharing)*** |

**For this submission, I have used the earlier assignments code-**

## Recall, Precision, and F1 Score

- ***Explanation of Recall, Precision, and F1 score***
Recall, Precision, F1 scores and the metrics used for classification problems best suited for binary classifications but can be extended to multiclass problems.
We need these scores as accuracy alone is not sufficient to represent models performance. Lets take an example to understand it better.

![Confusion Matrix](https://github.com/SachinDangayach/END2.0/blob/main/Session9/images/1_1.PNG)

TP = True Positive

TN = True Negative

FP = False Positive

FN = False Negative

A confusion matrix as mentioned above shows the actual verses predictions by any model. We have chosen a binary model (dog or no dog).

Accuracy = TP / (TP+FP+TN+FN)

Recall = TP / (TP+FN)

Precision = TP / (TP + FP)

F1 = 2 * ( Recall * Precision) / (Recall + Precision)

- ***Intuition***

![ALT](https://github.com/SachinDangayach/END2.0/blob/main/Session9/images/1_2.PNG)

Precision is to measure the quality of our predictions only based on what our predictor claims to be positive (regardless of all it might miss):

***Precision = All we predicted correctly / All we predicted, correctly or wrongly***

***Why precision is important then?*** Imagine our device is so stupid that it ALWAYS claims that “tomorrow is going to rain”! Then, surprisingly, it is not going to mis-predict one single rainy day! That means: Recall = 100%! Should I conclude that this is a perfect device? No, I should ask for precision now.

However, Recall is to measure such quality with respect to the mistakes we did (what should have been predicted as positive but we flagged as negative ):

***Recall = All we predicted correctly / All we should have predicted***

***Why Recall is important*** Suppose we have a weather forecasting device; to predict rainy days. If this device has a high precision, it means when it says “it is going to rain”, we can trust it. But this doesn’t give us any information about all the times it says “it is not going to rain”! If the false claims is going to be costly for our business, then we might want to ask about the number of times this device misses a rainy day.

***F1 Score*** represents the mean ( Harmonic mean) of recall and precision. We should be careful while using the F1 score and in general it gives equal weightage to both recall and precision though the importance of recall and precision could vary case by case as a model to predict a cancer patient will need to have high recall also.

We can extend the understanding to multiclass problems by a fine tweak of considering all the other classes as negative while making predictions and calculating recall/precision for a class.

- ***Implementation***

I used the prior code for sentiment analysis model and changed it to calculate recall, precision etc. for every epoch.

  - ***Dataset:*** stanfordSentimentTreebank

  - ***Model:*** RNN ( GRU )

  - ***Code snippet for metrics***

  ![ALT](https://github.com/SachinDangayach/END2.0/blob/main/Session9/images/1_3.PNG)

- ***Logs for last epochs***

  ![ALT](https://github.com/SachinDangayach/END2.0/blob/main/Session9/images/1_4.PNG)

  As we can see, Model training accuracy for epoch20 is just ~39%. It reflected in score metrics also as-

  we see, low precision (<.60) for all classes. It means whatever model is predicting has low confidence. Its doing lots of miss classification by classifying wrongly other sentiment to the one we are calculating score for.

  except one class, all scores for Recall are lesser than 60 showing model is not able to select all the relevant cases for a particular sentiment or in other words the model is missing to predict the sentiment class for many cases.

## BLEU

- ***Explanation of BLEU score***

BLEU (Bilingual Evaluation Understudy) score is a measure to present how many n-grams are present it the predicted score in comparison to the actual. It lies between 0 to 1 as max we can have is the case where the predicted and actual case are identical and thus we can find all possible n-grams (ordered sequence of words of specific length). BLUE4 counts n-grams up to length 4.

- ***Intuition***

We can assume that if the model is predicting absolutely as expected for a task like Q&A or language translation, the words and their order should be similar. Though this doesn't stands out as true assumption as two sentences could convey the same message while using different words and in different order also. For example, answer to the question, which is your favorite sports, one can answer, I like cricket and the other answer could be cricket is my favorite sport. Here we will have a very poor BLEU score though both convey same answer. On the contrary, I like soccer, will have high BLUE score though both are different answers. High BLEU score could be a good measure for specific cases like predicting the full form of a acronyms.

- ***Implementation***

I have used my existing code to predict the answer for a question. The model was not performing good and this will be reflected in BLEW score also.

  - ***Dataset:*** CMU Question Answer Dataset

  - ***Model:*** Encoder Decoder ( Seq2Seq Model )

![BLEU Score Implement](https://github.com/SachinDangayach/END2.0/blob/main/Session9/images/2_1.PNG)

- ***Logs***

![Training Logs](https://github.com/SachinDangayach/END2.0/blob/main/Session9/images/2_2.PNG)

We can see the BLEU score as to be as low as 0.05. This is due to the model not performing well for the task. With a better model with proper training, the scores should improve and the probabilities of finding similar n-grams in test and actual should increase.

## Perplexity

- ***Explanation of Perplexity score***

As we have can  see, the bleu score will become significantly lower as text size increase, to overcome this, we came up with idea of perplexity which can be thought of as the reciprocal of probability, normalized by the sequence of length. Perplexity is related to entropy in a way that adding more sentences introduces more uncertainty. So other things being equal a larger test set is likely to have a lower probability than a smaller one. Ideally, we’d like to have a metric that is independent of the size of the dataset. We could obtain this by normalizing the probability of the test set by the total number of words, which would give us a per-word measure.

We can interpret perplexity as the weighted branching factor. If we have a perplexity of 100, it means that whenever the model is trying to guess the next word it is as confused as if it had to pick between 100 word.

- ***Intuition***

Meaning of perplexity is confusion. As we have experienced, when a small kid starts talking, the words, and sentences are not clear during initial days. We will be many times confused or perplexed with what the kid is trying to convey. Over the period of time the kid will learn and improve and will start making correct sentences which are easy to comprehend. Going by the same analogy, when a model ( lets assume for language translation) is not trained properly the output will be confusing and this resulting high perplexity score. But, as the model learns better, we will start getting better output and thus less confusing output and hence the perplexity score will go down.

- ***Implementation***

I have used my existing code to predict the answer for a question. The model was not performing good and this will be reflected in Perplexity score also.

  - ***Dataset:*** CMU Question Answer Dataset

  - ***Model:*** Encoder Decoder ( Seq2Seq Model )

![Perplexity Score Implement](https://github.com/SachinDangayach/END2.0/blob/main/Session9/images/3_1.PNG)

- ***Logs***

![Training Logs](https://github.com/SachinDangayach/END2.0/blob/main/Session9/images/3_2.PNG)

We can see the Perplexity score (based on unigram) going down from epoch 1 to epoch 10 but still it is as high as 47 from training and 36 for test set. This is due to the model not performing well for the task. With a better model with proper training, the scores should go down and we should better results.

## BERTScore

- ***Explanation of BERTScore score***

- ***Intuition***
The basis of metrics like BERTScore etc. can be understood from the analogy like if a person has good understanding of physics and computer science and got many publications on his/her name, the chances of that person to be good in math is high. Using this analogy, if we use the prediction of model and actual text and both results similar results (in terms of embeddings) by BERT model, the chances of the model working good are very high.

- ***Implementation***

I have used my existing code to predict the answer for a question. The model was not performing good and this will be reflected in BERTScore also.

  - ***Dataset:*** CMU Question Answer Dataset ( I have reduced the dataset size due to hardware constraints)

  - ***Model:*** Encoder Decoder ( Seq2Seq Model )

I have used the standard bert_score package (code- from bert_score import score)

![BERTScore Implement](https://github.com/SachinDangayach/END2.0/blob/main/Session9/images/4_1.PNG)

- ***Logs***

![Training Logs](https://github.com/SachinDangayach/END2.0/blob/main/Session9/images/4_2.PNG)

We can see the train BERTScore F1 score as to be as low .5. This is due to the model not performing well for the task. With a better model with proper training, the scores should improve as in that case the model will have similar ( in meaning also) actual and predicted tokens list and thus it will generate similar embeddings resulting high bert scores.
Also, due to limited RAM, I was not able to calculate the BERTScore for more epochs and the system was crashing and hence I have kept it for only one epoch.
