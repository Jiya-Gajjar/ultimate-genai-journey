# Day 2 - Transformer Internals

# Bringing the Tensors into the picture in Transformers.

So basically the transformers work with the vectors(Tensors) instead of words.
 
Its work flow is:
1. Input Sentence.
2. Word Embeddings (n * 512).
3. Encoder.
    1. Self-Attention.
    2. Feed Forward Neural Network.
4. Output Tensor (n * 512).
5. Next Encoder.


*Lets Understand each step:*

1. **Input Sentence.**

The Transformer first will receive is the Input.

So, basically they are words and so Neural network cant proccess words so they need to converted into the Numerical vectors called Embeddings.

2. **Word Embeddings.**

Each word is now to be transformed into the Vectors(Embeddings) for further processing.

It is Transformed into 512 dimensional embbeding vector.

For Example:
I --> [0.21, 0.45, ...]
Love --> [0.78, 0.46, ...]
Animal --> [0.56, 0.45, ...]
Etc --> [...]

After this step, the sentences is represented as a list of vectors where every vector has 512 dimensions.

These embeddings are the input of the first encoder.

3. **Input to the Encoder**

Now the encoder input doesnt recieve the words, it recieve the vectors(Tensor).

And for a sentence with n words, the input size is:
n * 512

where,
n = number of the words in the sentences.
512 = embedding dimension.

4. **Flow Through the Encoder**

Each Encoder has two sub-layers.

Input Tensor
     |
     |
    \ /
Self-Attention
     |
     |
    \ /
Feed Forward Neural Network
     |
     |
    \ /
Output Tensor

The output tensor has the same shape as the input tensor.(n * 512)
So size remains Unchanged

5. **Multiple Encoder Layers**

As discussed before there are 6 Encoder in the original paper it can be more but for now let it be 6. So the output tensor from one encoder becomes the input tensor of the another encoder.

Embeddings
     |
     |
    \ /
Encoder 1
     |
     |
    \ /
Encoder 2
     |
     |
    \ /
Encoder 3
     |
     |
    \ /
Encoder 4
     |
     |
    \ /
Encoder 5
     |
     |
    \ /
Encoder 6


6. **Independent Word Paths**

Each word has its own path through the Encoders.

During Self-Attention Layer these paths interact with each other.
Each word can access information from every other word.

7. **Self-Attention**

Every word compares itself with all other words in the sentence.

8. **Feed-Forward Network**

FFN processes each word Indepnedently.
No interaction occurs in this layer with other words.

9. **Final Output**

The encoder outputs a new tensor of shape: n * 512


-------------------------------------------------




# 1. Word Embeddings

Computers cannot understand words directly.

Every input word is first converted into a numerical vector called an **Embedding Vector**.

These vectors capture the semantic meaning of words.

Words with similar meanings have similar embedding vectors.

### Example

```
Dog  → [0.24, 0.91, ...]
Cat  → [0.26, 0.88, ...]
Car  → [0.91, 0.10, ...]
```

Dog and Cat have similar vectors because their meanings are related.

---

# 2. Why do we need Embeddings?

Neural Networks only work with numbers.

Embeddings convert words into vectors while preserving their meanings.

Instead of treating words as IDs, embeddings allow the model to understand semantic relationships.

### Example

```
King - Man + Woman ≈ Queen
```

---

# 3. Positional Encoding

Unlike RNNs, Transformers process all words simultaneously.

Because of this, Transformers do not know the order of words.

To solve this problem, Positional Encoding is added to every embedding vector.

This tells the model where each word appears in the sentence.

### Example

Sentence:

```
I love AI
```

After positional encoding:

```
Embedding + Position Information
```

Now the model knows:

- "I" is first
- "love" is second
- "AI" is third

---

# 4. Bringing Tensors into the Picture

After embeddings and positional encoding are created, all word vectors are stacked together into a matrix called **X**.

Each row represents one word.

Example:

```
Word 1
Word 2
Word 3
Word 4
```

↓

```
Embedding Matrix (X)
```

The Transformer now processes the entire matrix instead of individual words.

This makes parallel computation possible.

---

# 5. Why are Embeddings converted into Query, Key and Value?

Embeddings contain general information about words.

However, Self-Attention requires three different roles:

- Query → What information am I looking for?
- Key → What information do I have?
- Value → What information should I pass?

Every embedding is multiplied by three trainable weight matrices.

```
Embedding

↓

WQ

↓

Query
```

```
Embedding

↓

WK

↓

Key
```

```
Embedding

↓

WV

↓

Value
```

These weight matrices are learned during training.

---

# 6. What is Self-Attention?

Self-Attention allows every word to look at every other word in the sentence.

It helps the model understand which words are important while processing the current word.

Example:

```
The animal didn't cross the street because it was tired.
```

When processing **it**, the model learns that **it** refers to **animal**, not **street**.

---

# 7. Steps of Self-Attention

### Step 1

Convert embeddings into Query, Key and Value vectors.

---

### Step 2

Calculate Attention Scores.

Every Query is compared with every Key using a Dot Product.

```
Score = Query × Key
```

Higher score means stronger relationship.

---

### Step 3

Scale the Scores.

Divide every score by:

```
√dk
```

This keeps gradients stable during training.

---

### Step 4

Apply Softmax.

Softmax converts scores into probabilities.

Properties:

- All values become positive.
- All probabilities add up to 1.

---

### Step 5

Multiply each Value vector by its attention weight.

Important words receive larger weights.

Less important words receive smaller weights.

---

### Step 6

Add all weighted Value vectors.

The final result becomes the new representation of that word.

---

# 8. Matrix Calculation of Self-Attention

Instead of processing one word at a time, Transformers process all words together using matrices.

```
Q = X × WQ

K = X × WK

V = X × WV
```

The complete attention equation is:

```
Attention(Q,K,V)

=

Softmax(QKᵀ / √dk)

×

V
```

This matrix implementation makes Transformers much faster.

---

# 9. Multi-Head Attention

Instead of using one attention mechanism, the Transformer uses multiple attention heads.

The original Transformer used **8 heads**.

Each head learns different relationships.

Example:

One head may learn:

Subject → Verb

Another head may learn:

Pronoun → Noun

Another head may learn:

Object → Verb

Each head creates its own Q, K and V matrices.

The outputs are concatenated together.

Finally they are multiplied by another weight matrix called:

```
WO
```

This produces one final output.

---

# 10. Residual Connections

Every sub-layer in the Transformer uses a Residual Connection.

Instead of only passing the new output,

the original input is added back.

```
Output

=

Input

+

Sub-layer Output
```

Residual Connections help information flow through deep networks.

They also reduce the vanishing gradient problem.

---

# 11. Layer Normalization

After every Residual Connection,

Layer Normalization is applied.

Its purpose is to keep values stable during training.

Benefits:

- Faster convergence
- Stable gradients
- Better training

---

# 12. Decoder Internals

The Decoder contains three sub-layers.

## Masked Self-Attention

The Decoder cannot see future words.

Only previously generated words are visible.

---

## Encoder-Decoder Attention

The Decoder looks at the Encoder's output.

This helps generate the correct output word.

Queries come from the Decoder.

Keys and Values come from the Encoder.

---

## Feed Forward Network

The Decoder also applies an FFN to every generated token independently.

---

# 13. Final Linear Layer

The Decoder outputs vectors.

These vectors cannot directly become words.

The Linear Layer converts every vector into a **Logits Vector**.

Each value corresponds to one word in the vocabulary.

---

# 14. Softmax

Softmax converts logits into probabilities.

The word with the highest probability is selected as the next output.

Example:

```
I : 0.03

am : 0.72

student : 0.12

teacher : 0.05
```

The model predicts:

```
am
```

---

# 15. Training

During training,

the model predicts the next word.

Its prediction is compared with the correct answer.

The difference is called the **Loss**.

The loss is used to update all trainable weights using Backpropagation.

As training continues,

predictions become more accurate.

---

# 16. Greedy Decoding

Greedy Decoding always selects the word with the highest probability.

Simple and fast.

However,

it may not always produce the best sentence.

---

# 17. Beam Search

Beam Search keeps multiple possible sentences instead of only one.

It compares different possibilities before choosing the final output.

This usually produces better translations than Greedy Decoding.

---


# Key Takeaways

- Words are converted into Embedding Vectors.
- Positional Encoding provides word order.
- Embeddings are transformed into Query, Key and Value vectors.
- Self-Attention helps words understand context.
- Matrix operations allow parallel computation.
- Multi-Head Attention learns different relationships.
- Residual Connections improve gradient flow.
- Layer Normalization stabilizes training.
- Decoder predicts one word at a time.
- Linear Layer converts vectors into logits.
- Softmax converts logits into probabilities.
- Training improves predictions using Backpropagation.
- Beam Search generally produces better outputs than Greedy Decoding.

---

# Interview Questions

1. What is an Embedding?
2. Why do we need Embeddings?
3. What is Positional Encoding?
4. Why can't Transformers understand word order?
5. Why are Embeddings converted into Query, Key and Value?
6. What is Query?
7. What is Key?
8. What is Value?
9. Explain Self-Attention step by step.
10. Why is Dot Product used?
11. Why divide by √dk?
12. Why is Softmax applied?
13. What is Matrix Self-Attention?
14. Why are matrices used?
15. What is Multi-Head Attention?
16. Why multiple heads instead of one?
17. What is WO?
18. What are Residual Connections?
19. Why is Layer Normalization required?
20. Explain the Decoder internals.
21. What is the Linear Layer?
22. What are Logits?
23. Why is Softmax used at the end?
24. What is Greedy Decoding?
25. What is Beam Search?
26. How is a Transformer trained?
27. What is Loss?
28. What is Backpropagation?
29. Explain the complete Transformer workflow.
30. Explain the Transformer in under one minute.




