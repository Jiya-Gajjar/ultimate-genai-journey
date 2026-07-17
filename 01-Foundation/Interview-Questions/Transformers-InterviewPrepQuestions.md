## Transformers Interview Questions

1. NLP Basics

What is NLP?
Why is NLP important?
What are some real-world applications of NLP?
What are sequences in NLP?
Why can't computers understand text directly?
Why do we convert text into numbers?
What are tokens?
What is tokenization?
Why do language models use tokens instead of words?
What are the limitations of traditional NLP methods?

2. Transformer Basics

What is a Transformer?
Why was the Transformer introduced?
What problems does it solve?
Why is it called a Transformer?
What are the two main components of a Transformer?
Explain the overall Transformer architecture.
What is the purpose of a Transformer?
What are the advantages of Transformers?
What are the disadvantages of Transformers?
Where are Transformers used?
Why are Transformers considered state-of-the-art?
What is sequence-to-sequence learning?
What tasks can Transformers perform?

3. RNN vs LSTM vs Transformer

What is an RNN?
What is an LSTM?
Why were RNNs popular?
What are the problems with RNNs?
What are long-term dependencies?
What is the vanishing gradient problem?
What is the exploding gradient problem?
Why are LSTMs better than RNNs?
Why are Transformers better than LSTMs?
Why can Transformers process data in parallel?
Why are RNNs sequential?
Compare RNN, LSTM, and Transformer.
Which architecture is faster?
Which architecture performs better on long sequences?
Which architecture is easier to parallelize?

4. Encoder

What is an Encoder?
What is the purpose of the Encoder?
What are the sublayers of an Encoder?
Why are multiple Encoder layers stacked?
How many Encoder layers were used in the original paper?
Does every Encoder layer perform the same operations?
What is passed from one Encoder layer to the next?
What is the output of the Encoder?
Why is the Encoder important?
Can a Transformer work without an Encoder?

5. Decoder

What is a Decoder?
What is the purpose of the Decoder?
What are the sublayers of the Decoder?
Why is the Decoder different from the Encoder?
Why does the Decoder generate one token at a time?
What information does the Decoder receive?
What is passed from the Encoder to the Decoder?
Can a Decoder work without an Encoder?
Why does GPT only use a Decoder?
How does the Decoder know when to stop generating?

6. Embeddings

What is an embedding?
Why are embeddings required?
What is an embedding vector?
Why are words converted into vectors?
Why can't models work directly on text?
What information do embeddings contain?
Why are embeddings dense vectors?
What is embedding size?
Why was embedding size 512 in the original Transformer?
Are embeddings learned?
How are embeddings initialized?
What happens after embeddings are created?

7. Positional Encoding

Why is positional encoding needed?
Why can't Transformers understand word order naturally?
What is positional encoding?
Where is positional encoding added?
Why is it added instead of concatenated?
Why are sine and cosine functions used?
What information does positional encoding provide?
Can positional encoding generalize to longer sequences?
What happens if positional encoding is removed?
Is positional encoding learned or fixed?
What are learned positional embeddings?

8. Self-Attention

What is Self-Attention?
Why is it called Self-Attention?
Why is Self-Attention important?
How does Self-Attention work?
Explain Self-Attention step by step.
Why does every word attend to every other word?
What is context?
Why is context important?
How does Self-Attention capture context?
What is the output of Self-Attention?
Why is Self-Attention bidirectional?
How does Self-Attention differ from recurrence?
What happens after Self-Attention?

9. Query, Key, Value (QKV)

What is a Query vector?
What is a Key vector?
What is a Value vector?
Why are embeddings converted into Q, K, and V?
Why are three different vectors needed?
How are Q, K, and V created?
What are WQ, WK, and WV?
Are WQ, WK, and WV trainable?
Why are Q, K, and V smaller than embeddings?
Can Q, K, and V have the same dimensions as embeddings?
What is the role of the Query?
What is the role of the Key?
What is the role of the Value?
Why can't embeddings be used directly?
How do Query and Key interact?
How is Value used?
What happens if Query and Key are identical?
What information does each vector carry?

10. Attention Score Calculation

How is the attention score calculated?
Why is dot product used?
What does a higher attention score mean?
What happens after calculating attention scores?
Why are scores divided by √dk?
What is dk?
What happens if scaling is not applied?
Why is Softmax used?
Why do Softmax outputs sum to 1?
What happens after Softmax?
Why are Value vectors multiplied by attention weights?
How is the final attention output calculated?
What is Scaled Dot Product Attention?

11. Matrix Calculation

Why is matrix multiplication used?
What is matrix X?
How are Q, K, and V matrices created?
What is the formula for Self-Attention?
Why is matrix implementation faster?
Why are all words processed simultaneously?
What dimensions do Q, K, and V have?
What is the attention matrix?

12. Multi-Head Attention

What is Multi-Head Attention?
Why is Multi-Head Attention used?
Why are multiple heads better than one?
How many heads were used in the original paper?
Does every head learn the same thing?
What does each attention head learn?
What are separate Q, K, and V matrices?
Why are different weight matrices used?
What happens after all heads finish?
Why are outputs concatenated?
What is WO?
Why is WO required?
What would happen if there was only one attention head?
What are representation subspaces?

13. Feed Forward Network (FFN)

What is a Feed Forward Network?
Why is FFN required?
What happens inside the FFN?
Is the FFN shared across all tokens?
Why is FFN applied after attention?
Does FFN process tokens independently?

14. Residual Connections

What is a Residual Connection?
Why are Residual Connections used?
What problems do they solve?
What is a skip connection?
Where are Residual Connections used?

15. Layer Normalization

What is Layer Normalization?
Why is Layer Normalization required?
Why is LayerNorm applied after Residual Connection?
What problems does LayerNorm solve?

16. Decoder Attention

What is Masked Self-Attention?
Why is masking required?
Why can't the Decoder see future tokens?
What happens if masking is removed?
What is Encoder-Decoder Attention?
What is Cross Attention?
Where do Queries come from in Cross Attention?
Where do Keys come from?
Where do Values come from?
Difference between Self-Attention and Cross Attention.
Difference between Encoder Self-Attention and Decoder Self-Attention.

17. Linear Layer & Softmax

What is the Linear layer?
Why is the Linear layer required?
What are logits?
What is vocabulary size?
Why is the output vector equal to vocabulary size?
What is Softmax?
Why is Softmax applied?
What does Softmax produce?
How is the next word selected?

18. Training

How is a Transformer trained?
What is a forward pass?
What is one-hot encoding?
What is the loss function?
What is Cross Entropy Loss?
Why is loss calculated?
What is backpropagation?
How are weights updated?
Why does training require labeled data?

19. Decoding

What is Greedy Decoding?
What are its advantages?
What are its disadvantages?
What is Beam Search?
Why is Beam Search better than Greedy Search?
What is beam width?
When should Beam Search be used?

20. Comparisons

Encoder vs Decoder.
Self-Attention vs Cross Attention.
Self-Attention vs Masked Self-Attention.
FFN vs Self-Attention.
Embeddings vs Positional Encoding.
Greedy Search vs Beam Search.
Transformer vs RNN.
Transformer vs LSTM.
BERT vs GPT (basic).
Encoder-only vs Decoder-only models.

21. Big Tech / FAANG Questions

Explain a Transformer in one minute.
Explain Self-Attention in one minute.
Explain Self-Attention to a five-year-old.
Explain the complete Transformer architecture.
Explain the data flow inside a Transformer.
Why are Transformers parallel?
Why do Transformers perform better than RNNs?
Why are embeddings needed?
Why is positional encoding needed?
Why do we need Q, K, and V?
Why divide attention scores by √dk?
Why is Softmax used?
Why is Multi-Head Attention better?
Why are Residual Connections important?
Why is LayerNorm needed?
Why does GPT only use the Decoder?
Why does BERT only use the Encoder?
Draw the complete Transformer architecture.
Draw the Encoder block.
Draw the Decoder block.
Draw the Self-Attention mechanism.
Explain how a sentence is translated using a Transformer.

22. Rapid Fire

What is attention?
What is context?
What is a token?
What is a vector?
What is an embedding?
What is a Query?
What is a Key?
What is a Value?
What is masking?
What is a logit?
What is Softmax?
What is LayerNorm?
What is FFN?
What is Cross Attention?
What is Beam Search?
What is Greedy Search?
What is one-hot encoding?
What is vocabulary?
What is parallelization?
Why are Transformers so successful?