## Converting text into numbers

To be able to process the data in the model, we need to convert the text into numbers. We want to encode word tokens, each into som vector that represents a point in some sort of word space.

The most common techniques:
- **one hot encoding**
- **word tokenization** a straight mapping from word or character or sub-word to a numerical value.

There are three main leves of tokenization:
- Using word-level tokenization with the sentence "I love TensorFlow" might result in "I" being 0, "love" being 1 and "TensorFlow" being 2. In this case, every word in a sequence considered a single token.

- Character-level tokenization, such as converting the letters A-Z to values 1-26. In this case, every character in a sequence considered a single token.

- Sub-word tokenization is in between word-level and character-level tokenization. It involves breaking invidual words into smaller parts and then converting those smaller parts into numbers. For example, "my favourite food is pineapple pizza" might become "my, fav, avour, rite, fo, oo, od, is, pin, ine, app, le, piz, za". After doing this, these sub-words would then be mapped to a numerical value. In this case, every word could be considered multiple tokens.

### Word Tokenization in Tensorflow

The next block of code show how to create a method that tokenize the data.

```python
 import tensorflow as tf 
 from tensorflow.keras.layers.preprocessing import TextVectorization

 text_vectorizer = TextVectorization(
     max_tokens = None, #HOW MANY WORDS IN THE VOCABOULARY
     standardize = "lower_and_strip_punctuation", #HOW TO PROCESS TEXT
     split = "whitespace", #HOW TO SPLIT TOKENS
     output_mode = "int", #how to map tokens to numbers
     output_sequence_length = None,#HOW LONG SHOULD BE THE OUTPUT SEQUENCE 

 )

 #FIT THE TEXT VECTORIZER TO THE TRAINING TEXT
 text_vectorizer.adapt(train_sentences)
```
For more information we suggest you to check the official documentation at 
[Tensorflow](https://www.tensorflow.org/api_docs/python/tf/keras/layers/TextVectorization) .

----
## Embeddings 

An embedding is a representation of natural language which can be learned. Representation comes in the form of a feature vector. For example, the word "dance" could be represented by the 5-dimensional vector [-0.8547, 0.4559, -0.3332, 0.9877, 0.1112]. It's important to note here, the size of the feature vector is tuneable. There are two ways to use embeddings:
- **Create your own embedding** - Once your text has been turned into numbers (required for an embedding), you can put them through an embedding layer (such as tf.keras.layers.Embedding) and an embedding representation will be learned during model training.
- **Reuse a pre-learned embedding** - Many pre-trained embeddings exist online. These pre-trained embeddings have often been learned on large corpuses of text (such as all of Wikipedia) and thus have a good underlying representation of natural language. You can use a pre-trained embedding to initialize your model and fine-tune it to your own specific task.

### Embeddings in Tensorflow

The next block of code show how to create an embedding layer.

```python
 import tensorflow as tf 
 from tensorflow.keras import layers

embedding = layers.Embedding(
    input_dim = max_vocab_length,#SET INPUT SHAPE
    output_dim = 128,#SIZE OF THE EMBEDDING VECTOR
    embeddings_initializer = "uniform",#INITIALIZE RANDOMLY
    input_length = max_length, #HOW LONGTH IS EACH INPUT
    name = "embedding_1",#NAME OF THE LAYER
)
```
For more information we suggest you to check the official documentation at 
[Tensorflow](https://www.tensorflow.org/api_docs/python/tf/keras/layers/Embeddingn) .

