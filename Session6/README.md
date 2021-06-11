
### Submission by:
1. Sachin Dangayach (sachin.dangayach@gmail.com)

***[Link for colab file](https://colab.research.google.com/drive/1yYliDdo2Tf6rmWDKDBDPAixfnHkjlDmy?usp=sharing)***

# Objective

We aim to build a network that would:

1. Take the last code  (+tweet dataset) and convert that in such a war that:
  - encoder: an RNN/LSTM layer takes the words in a sentence one by one and finally converts them into a single vector. VERY IMPORTANT TO MAKE THIS SINGLE VECTOR
    this single vector is then sent to another RNN/LSTM that also takes the last prediction as its second input. Then we take the final vector from this Cell
    and send this final vector to a Linear Layer and make the final prediction.
  - This is how it will look:

    - embedding
    - word from a sentence +last hidden vector -> encoder -> single vector
    - single vector + last hidden vector -> decoder -> single vector
    - single vector -> FC layer -> Prediction

  - Your code will be checked for plagiarism, and if we find that you have copied from the internet, then -100%.
  - The code needs to look as simple as possible, the focus is on making encoder/decoder classes and how to link objects together
  - Getting good accuracy is NOT the target, but must achieve at least 45% or more
  - Once the model is trained, take one sentence, "print the outputs" of the encoder for each step and "print the outputs" for each step of the decoder. ← THIS IS THE ACTUAL ASSIGNMENT


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
    - num_epochs = 1
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

![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session6/Images/Train_Logs.png)

- Accuracy and Loss plots
![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session6/Images/Acc_Loss_plotss.png)

### Model results on manually / test dataset
![alt](https://github.com/SachinDangayach/END2.0/blob/main/Session6/Images/output.png)
