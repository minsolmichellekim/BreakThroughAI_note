Recurrent Neural Networks 
- Feedforward NN are not ideal for data such as text that are sequential and context dependent.
- As an alternative, RNN iteratively apply same base operation (RNN cell) to each element in input sequence
- RNN cells are 'memory' as it helps capture information about what has been calculated so far from previous inputs.
- It keeps track of hidden state variable and uses hidden state variable to encode sequential information 

Encoder: NN taking in sequence of words (represented using word embeddings) and outputs vector or code that can be viewed as a summary of input sequence
Decoder: NN taking vector output of encoder and turning into scalar or sequence of outputs (words represented by word embeddings, depending on application)

<img width="778" alt="Screenshot 2023-07-25 at 9 56 29 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/bdf38181-ce91-4def-9117-0fe4a65b8631">

<img width="811" alt="Screenshot 2023-07-25 at 9 56 40 PM" src="https://github.com/michellekimgit/BreakThroughAI_note/assets/94397733/12f5ef3d-6886-4903-a39a-55dd2174eafa">
