
### Submission by:
1. Sachin Dangayach (sachin.dangayach@gmail.com)

# Objective

We aim to refactor the (repo)[https://github.com/bentrevett/pytorch-seq2seq] (assignment 2 and 3) while following the conditions below - :

1.  Use none of the legacy stuff
2.  MUST use Multi30k dataset from torchtext
3.  Use yield_token, and other code that we wrote

# Solution

***Please refer to the refactored code link to go to the code in colab***

| Old Repo Link | Refactored Code Colab Link     | Description                |
| :-------- | :------- | :------------------------- |
| [Repo - 2](https://github.com/bentrevett/pytorch-seq2seq/blob/master/2%20-%20Learning%20Phrase%20Representations%20using%20RNN%20Encoder-Decoder%20for%20Statistical%20Machine%20Translation.ipynb) |[Colab Link - 1](https://colab.research.google.com/drive/11i_lWIs882O73y-slKpLsoy46QzHVU78?usp=sharing)| ***Learning Phrase Representations using RNN Encoder-Decoder for Statistical Machine Translation*** |
| [Repo - 3](https://github.com/bentrevett/pytorch-seq2seq/blob/master/3%20-%20Neural%20Machine%20Translation%20by%20Jointly%20Learning%20to%20Align%20and%20Translate.ipynb) | [Colab Link - 2](https://colab.research.google.com/drive/1uuPBlWulzJh_5vwTYWyvy5QKJywNSTIC?usp=sharing) | ***Neural Machine Translation by Jointly Learning to Align and Translate*** |

# Key Functions and steps

- ***get_tokenizer*** : Takes tokenizer function and language as input and generate tokenizer function for a string sentence

- ***yield_tokens*** : Helper function to yield list of tokens. It takes iterable and language key as input and returns the list of tokens as output using the generated tokenizer function.

- ***Train, Test Iterators*** : Used Multi30k dataset from torchtext.datasets for Train, Test Iterators.

- ***Vocab Object*** : Used build_vocab_from_iterator from torchtext.vocab to create object of Vocab class.

- ***Transformations*** : Created helper functions for Transformations like
  - sequential_transforms: helper function to club together sequential operations
  - tensor_transform: function to add BOS/EOS and create tensor for input sequence indices
  - src and tgt language text transforms to convert raw strings into tensors indices

- ***collate_fn*** : function to collate data samples into batch tensors

- Created dataloaders using train, test Iterators

- ***Created models as mentioned in the repo and made the code working without any legacy code***
