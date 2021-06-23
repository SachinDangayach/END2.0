
### Submission by:
1. Sachin Dangayach (sachin.dangayach@gmail.com)

***[Link for colab file](https://colab.research.google.com/drive/1CjHaQtXo2AVu4qzOG_UHGALelhUYI1mR?usp=sharing)***

***[Link for colab file](https://colab.research.google.com/drive/1gVaUJifS7v8QNe0bO7NoEaKC05Ruv4lY?usp=sharing)***

# Objective

Assignment has got 3 parts as mentioned below along with respective solutions:

## 1. Part 1: Submit the Assignment 5 again as mentioned below.

  - Only use datasetSentences.txt. (no augmentation required)
  - Your dataset must have around 12k examples.
  - Split Dataset into 70/30 Train and Test (no validation)
  - Convert floating-point labels into 5 classes (0-0.2, 0.2-0.4, 0.4-0.6, 0.6-0.8, 0.8-1.0)

## Solution:

***[Link for colab file for Session7 part 1 submission](https://colab.research.google.com/drive/1B6LeAUgkW0q90NuaVIdK8cZ8ZOTi2M_Q?usp=sharing)***

  I have done the Assignment 5 by using the python package ***pytreebank*** to get the dataset. Below is the earlier submission link-

***[Prior Submission - Assignment 5 - colab](https://colab.research.google.com/drive/13-mpSe80XXG69Pz3y1SOP7HQmekAyggw?usp=sharing)***

***[Prior Submission - Assignment 5 - Git Readme](https://github.com/SachinDangayach/END2.0/blob/main/Session5/README.md)***

**For this submission, we have prepared the dataset directly as explained in the steps below-**

  # Data

  1. We get the data files from the repo by link http://nlp.stanford.edu/~socherr/stanfordSentimentTreebank.zip. This is a popular dataset for benchmarking the sentiment analysis models. Sentences are broken into phrases and users have manually given the sentiment (5 classes from very negative to very positive) to each of these phrases which are the constituents of the sentences. we can see the breakdown tree structure of an example.

  ![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session7/Utils/Part1/SST_Tree.png)

  2. Once we get the data and unzip the files, we start preparing the dataframes for multiple files we have got.

  - Get sentiment values for phrases and convert label values to 5 buckets.

  ![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session7/Utils/Part1/img1.PNG)

  ![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session7/Utils/Part1/img2.PNG)

  - Get all sentences in a dataframe.

  ![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session7/Utils/Part1/img3.PNG)

  - Get the dictionary which contains all phrases and respective phrase ids.

  ![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session7/Utils/Part1/img4.PNG)

  - In this dataset, each sentence is split into lowest level phrases/tokens and these phrases are provided the sentiments. These leaf level nodes are merged to get the sentiment of next level and this goes up till the entire sentence. Hence the dictionary contains all sentences with the sentiment as top level phrase or node. We can do an inner join to find these phrases.

  ![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session7/Utils/Part1/img5.PNG)

  - As we need to get the sentiment of the sentences and sentiments are maintained at phrase level, we will do the inner join to get the sentiment of sentences using the dataframe from above step.

  ![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session7/Utils/Part1/img6.png)

  - To get the train test split, we will not use the train_test split dataset which has got the sentence index and split label and instead we will split the data into 70:30 ratio directly

  ![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session7/Utils/Part1/img7.PNG)


  # The Network / Model - Architecture

  We have created as language model which is also a language model as it looks the entire sentence before predicting the sentiments.
  below are the three classes-

  1. Encoder : We have used LSTMCell here so that we can unroll the RNN word by word for a given tweet. We collect the output and stack them. The final hidden state and cell state are returned along with output
  ![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session6/Images/encoder.PNG)

  2. Decoder : Decoder takes the output from encoder as input along with last hidden and cell state as initial hidden and cell states. It runs for 1 step and its hidden state is fed to a Fully connected layer to give the output prediction vector.
  ![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session6/Images/decoder.PNG)

  3. Seq2Seq : It connects both encode and decoder and results the prediction vector
  ![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session6/Images/seq2seq.png)

  # The Network parameters

  - Training hyperparameters
      - num_epochs = 10
      - learning_rate = 0.001
      - batch_size = 8

  -  Model hyperparameters
      - input_size_encoder = len(TEXT.vocab)
      - input_size_decoder = 64 # Hidden dimention for output
      - output_size = len(LABEL.vocab)
      - encoder_embedding_size = 32
      - cell_state_size = 64
      - hidden_size = 64
      - num_layers = 1

  # The training
  Model achieves above 70% accuracy in less than 5 epochs
  - Training Log

  ![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session6/Images/Train_logs.png)

  - Accuracy and Loss plots

  ![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session6/Images/Acc_Loss_plots.png)

  ### Model results on manually / test dataset
  ![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session6/Images/output1.png)
  ![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session6/Images/output2.png)









2. Part  2: Train model we wrote in the class on the following two datasets taken from this links below:
  - http://www.cs.cmu.edu/~ark/QA-data/ (Links to an external site.)
  - https://quoradata.quora.com/First-Quora-Dataset-Release-Question-Pairs

3. Try for additional datasets the same activity what we tried above from the link mentioned below:
  - https://kili-technology.com/blog/chatbot-training-datasets


# Data
1. We load the tweet.csv file in dataframe explore the dataset

![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session6/Images/dataset.png)

2. We clean the data and create the datasets with 70:30 train test split, and created the vocabs


# The Network / Model - Architecture

We have created as language model which is also a language model as it looks the entire sentence before predicting the sentiments.
below are the three classes-

1. Encoder : We have used LSTMCell here so that we can unroll the RNN word by word for a given tweet. We collect the output and stack them. The final hidden state and cell state are returned along with output
![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session6/Images/encoder.png)

2. Decoder : Decoder takes the output from encoder as input along with last hidden and cell state as initial hidden and cell states. It runs for 1 step and its hidden state is fed to a Fully connected layer to give the output prediction vector.
![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session6/Images/decoder.png)

3. Seq2Seq : It connects both encode and decoder and results the prediction vector
![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session6/Images/seq2seq.png)

# The Network parameters

- Training hyperparameters
    - num_epochs = 10
    - learning_rate = 0.001
    - batch_size = 8

-  Model hyperparameters
    - input_size_encoder = len(TEXT.vocab)
    - input_size_decoder = 64 # Hidden dimention for output
    - output_size = len(LABEL.vocab)
    - encoder_embedding_size = 32
    - cell_state_size = 64
    - hidden_size = 64
    - num_layers = 1

# The training
Model achieves above 70% accuracy in less than 5 epochs
- Training Log

![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session6/Images/Train_logs.png)

- Accuracy and Loss plots

![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session6/Images/Acc_Loss_plots.png)

### Model results on manually / test dataset
![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session6/Images/output1.png)
![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session6/Images/output2.png)
