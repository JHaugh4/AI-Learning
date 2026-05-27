# Glossary and Notation

As per usual there is plenty of variation in what people call things and how they denote them, this is just a place to centralize the concepts and show some commonly used notation.

#### Tokenization and Embedding (Chapter 2)

$V = \lbrace \text{vocabulary tokens} \rbrace$
- The set of all vocabulary tokens.

$|V| :$ number of tokens in the vocabulary.
- `torch` calls it `num_embeddings`.
- SR calls it `vocab_size`.
- With `tiktoken`'s "gpt2" tokenizer $|V| = 50,257$.

$d:$ Dimensionality of embedding vectors, ie $\mathbf{e} \in \mathbb{R}^d$.
- `torch` calls it `embedding_dim`.
- SR calls it `output_dim` in chapter 2.

$T :$ context size.
- Also the sequence length.
- There's some subtlety here, but for absolute positional encodings, context size = sequence length.
- SR calls it the `context_length`.

$\mathbf 1_i \in \mathbb{R}^n$
- A one-hot vector: every entry is 0 except for exactly one 1.

$\mathbf{x}_i = \mathbf{1}_i \in \mathbb{R}^{|V|}$
- A token, represented as a one-hot vector.
- Note that from the a theoretical perspective, we think of the one hot vector $\mathbf x_i$ as the input to the network (a sample). We let someone else (the tokenizer) figure out how to get a one-hot vector. But we're going to learn the embedding matrix $W_E$, so it's part of the model - we don't take embedding vectors as inputs, we take one-hot vectors.

$W_E \in \mathbb{R}^{|V| \times d}$
- Embedding matrix, contains as rows the embedding vector for each token.
- $\mathbf{e}_i = \mathbf{x}_iW_E$
- Equivalent to the look-up table SR calls the `token_embedding_layer`.

$W_P \in \mathbb{R}^{T \times d}$
- Positional embedding matrix.
- Equivalent to the look-up table SR calls the `pos_embedding_layer`.

$X \in \mathbb{R}^{T \times |V|}$
- An input sequence of one-hot token vectors.

$H^{(0)} = XW_E + W_P$
- The input to the first hidden layer.
- $H^{(0)} \in \mathbb{R}^{T \times d}$
- Take the one-hot encoded input $X$ (a sequence of one-hot vectors) and look up each embedding vector in $W_E$, then add the positional encoding vectors stored as rows in $W_P$.
- This is the mathematical equivalent of
	`input_embeddings = token_embedding_layer(inputs) + pos_embedding_layer`.


#### Attention (Chapter 3)

$\mathbf x_i \in \mathbb{R}^d$
- A single embedding vector, which is the $i$-th element of the input sequence to an attention block.
- SR denotes it by $x^{(i)}$ and calls it a token vector.

$XX^T$
- Computes all pairwise dot products for the rows of $X$.
- $(XX^T)_{ij} = \mathbf x_i \cdot \mathbf x_j = \mathbf x_i^T \mathbf x_j$.

$\sigma (\mathbf z)_i = \dfrac{e^{z_i}}{\sum_{j=1}^{K} e^{z_j}}$
- The softmax function.
- Where $\mathbf z \in \mathbb{R}^K$.

$w_{ij}$
- In the "simplified" attention block: the attention score for a query $\mathbf x_i$ with respect to input $\mathbf x_j$.
- In the "standard" attention block: we project into the key and query spaces before computing the attention score.
- $\mathbf w_i \in \mathbb{R}^T$ contains the attention score for query $i$ with respect to all inputs in the context.

$a_{ij}$
- Attention weight for a query $\mathbf x_i$ and input $\mathbf x_j$.
- Attention weights are arrived at by normalizing attention scores with respect to a query, eg if we normalized by just dividing by row sum, $a_{21} = \dfrac{w_{21}}{\displaystyle \sum_j w_{2j}}$.
- In practice we use softmax to normalize: $\mathbf a_i = \sigma(\mathbf w_i)$.
- In the scaled dot product transformer architecture, we would instead project 

$W_q \in \mathbb{R}^{d \times d}$
- The query weight matrix.
- There is a single query weight matrix for each attention head.

$\mathbf q_i = \mathbf x_i W_q \in \mathbb{R}^d$
- The query vector for the $i$-th input embedding vector $\mathbf x_i$.

$W_k$
- The key weight matrix.

$W_v$
- The value weight matrix.

#### Misc.


$\mathbf{e}_i \in \mathbb{R}^d$
- The $i$-th embedding vector in a sequence $E$.

$E \in \mathbb{R}^{T \times d}$
- An input sequence of $T$ embedding vectors each of length $d$.
- $E = \begin{bmatrix} \mathbf{e}_1 \\ \mathbf{e}_2 \\ \vdots \\ \mathbf{e}_d \end{bmatrix}$.


There are two dimensionality expansions
- Extending a single token to a sequence.
- Extending a single sequence to a batch.
- E.g. $\mathbf e \in \mathbb{R}^d \to E \in \mathbb{R}^{T \times d} \to E \in \mathbb{R}^{B \times T \times d}$
	- Not sure about the dimensionality order of the batch tensor, but this matches the pattern.