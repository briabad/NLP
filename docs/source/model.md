## Ceate a RNN model

In this section we guide you throught the most common cells to made up a RNN model. The las section show you a different way to connect the cells and its beneffits 

[LSTM](#LSTM)

[GRU](#GRU)

[Bidirectional layers](#Bidirectionallayers)

---

## LSTM

The Long Short-Term Memory, or LSTM, is a recurrent neural network that is comprised of internal gates.

Unlike other recurrent neural networks, the network’s internal gates allow the model to be trained successfully using backpropagation through time, and avoid the vanishing gradients problem.


![LSTM PICTURE](https://miro.medium.com/max/1400/1*ahafyNt0Ph_J6Ed9_2hvdg.png)


Before we jump into the specific gates and all the math behind them, I need to point out that there are two types of normalizing equations that are being used in the **LSTM**. The first is the **_sigmoid function_** (represented with a lower-case sigma), and the second is the **_tanh function_**. This is a deliberate choice that has a very intuitive explanation.
Whenever you see a **_sigmoid function_** in a mechanism, it means that the mechanism is trying to calculate a set of scalars by which to multiply (amplify / diminish) something else (apart from preventing vanishing / exploding gradients, of course).
Whenever you see a **_tanh function_**, it means that the mechanism is trying to transform the data into a normalized encoding of the data.

## Step-by-Step LSTM Walk Through

### Forgat gate

![forgat gate](https://cdn.analyticsvidhya.com/wp-content/uploads/2017/12/10131319/14.png)
The first step in our LSTM is to decide what information we’re going to throw away from the cell state. This decision is made by a sigmoid layer called the “forget gate layer.” It looks at ht−1 and xt, and outputs a number between 0 and 1 for each number in the cell state Ct−1. A 1 represents “completely keep this” while a 0 represents “completely get rid of this.”

![forgat gate](https://miro.medium.com/max/1400/1*GjehOa513_BgpDDP6Vkw2Q.gif)

### Input gate
![input gate](https://cdn.analyticsvidhya.com/wp-content/uploads/2017/12/10131330/16.png )
The next step is to decide what new information we’re going to store in the cell state. This has two parts. First, a sigmoid layer called the “input gate layer” decides which values we’ll update. Next, a tanh layer creates a vector of new candidate values, C~t, that could be added to the state. In the next step, we’ll combine these two to create an update to the state.
![input gate](https://miro.medium.com/max/1400/1*TTmYy7Sy8uUXxUXfzmoKbA.gif)

### Output gate
![output gate](https://cdn.analyticsvidhya.com/wp-content/uploads/2017/12/10131340/18.png )
Finally, we need to decide what we’re going to output. This output will be based on our cell state, but will be a filtered version. First, we run a sigmoid layer which decides what parts of the cell state we’re going to output. Then, we put the cell state through tanh (to push the values to be between −1 and 1) and multiply it by the output of the sigmoid gate, so that we only output the parts we decided to.

![output gate](https://miro.medium.com/max/1400/1*VOXRGhOShoWWks6ouoDN3Q.gif )


For more information related with the LSTM cells, check:
https://www.analyticsvidhya.com/blog/2017/12/fundamentals-of-deep-learning-introduction-to-lstm/
https://towardsdatascience.com/illustrated-guide-to-lstms-and-gru-s-a-step-by-step-explanation-44e9eb85bf21
https://medium.com/analytics-vidhya/lstms-explained-a-complete-technically-accurate-conceptual-guide-with-keras-2a650327e8f2

---
## GRU
---
## Bidirectional Layers