
### Submission by:
1. Sachin Dangayach (sachin.dangayach@gmail.com)

***[Link for colab file](https://colab.research.google.com/drive/13-mpSe80XXG69Pz3y1SOP7HQmekAyggw?usp=sharing)***

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



# The Network / Model - Architecture



# The Network / Model - Loss Function



# The training



### ACCURACY ACHIEVED -



### Model results on manually / test dataset
