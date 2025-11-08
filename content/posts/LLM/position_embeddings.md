---
title: 'Positional & Input Embeddings (Data Preprocessing)'
date: 2025-11-07
draft:  false
featured: false  
description: "LLM - Positional Embeddings"
thumbnail: "/posts/LLM/images/position.png"
featureImage: "/posts/LLM/images/position.png" 
shareImage: "/posts/LLM/images/position.png"
author: "Angel Vyas"
tags:
    - llm
categories:     
    - llm
---

# 📘3. Positional Embeddings

## 🧠 Why Do We Need Positional Embeddings?

In `embedding layer`, the `same tokens` get mapped to the same `vector representation`.
That means the model naturally **has no idea about token order**.

For example, consider these two sentences:

- ✅ *Dog bites man*  
- ❌ *Man bites dog*

Same words, totally different meaning — because of word order.

So the model must somehow know which token came first, second, third, etc.

That’s exactly what positional embeddings do. ✅

👉 **Positional embeddings solve this** by adding information about the *position of each token* in the sequence — letting the model know **who comes first, second, etc.**

---

## 🧩 Types of Positional Embeddings

Positional embeddings come in two main types:

### 1. **Absolute Positional Embeddings**

Each token position (e.g., 0, 1, 2, …) gets its **own learned embedding vector**.

Example:
| Position | Embedding Vector (simplified) |
|-----------|------------------------------|
| 0 | [0.12, -0.45, 0.33, …] |
| 1 | [0.56, 0.11, -0.07, …] |
| 2 | [-0.22, 0.43, 0.88, …] |

So the embedding for position 0 always means “first token,” position 1 means “second token,” and so on.

📌 Used in: **GPT models (GPT-1, GPT-2, GPT-3)**  
In these models, absolute position embeddings are **learned** along with token embeddings — they are trainable parameters optimized during model training.

🧠 **Limitation:**  
They only work for sequence lengths seen during training.  
If a model was trained on 512 tokens, it can’t easily generalize to 1024-token sequences because positions beyond 512 have no embeddings.


### 2. **Relative Positional Embeddings**

Instead of representing **absolute position**, they encode **the distance between tokens**.

For example:
> “This token is 3 steps after that token.”

So, even if the sequence gets longer, the *relative distances* stay meaningful.

✅ **Advantage:** Works for variable-length or longer sequences not seen during training.  
💡 Used in: **Transformer-XL, T5, DeBERTa**, and modern architectures like **GPT-NeoX** or **Llama** (with rotary embeddings).

---

## ⚙️ Dimension of Positional Vectors

The **dimension of positional embeddings** is always the **same as the token embeddings**.

This allows simple addition:
```python
input_embeddings = token_embeddings + positional_embeddings
```

---
##  Input Embeddings
In modern transformer-based models, the **final input embedding** is formed by combining two components:

```
**Input Embedding = Token Embedding + Positional Embedding**
```

---

## 🧪 Implementing Positional & Input Embeddings (Hands-On)



- 🧩 **Batch size** = number of sequences processed in parallel (e.g., 8).  
- 📏 **Context length** = number of tokens per sequence (e.g., 4).  
- 🔢 **Embedding dimension** = size of each token or position vector (e.g., 256).

So, before adding positional embeddings:

`Input shape (token IDs): [8, 4]`

- Each of the 8 sequences contains 4 tokens.
- Each token is mapped to a **256-dimensional vector** by the token embedding layer:

`Token embeddings shape: [8, 4, 256]`

- Positional embeddings also have the same shape `[4, 256]` (one per position).  
  When added, they are **broadcasted** across the batch, i.e., added to every token in all 8 sequences.

After combining token + positional embeddings:

`Final input embedding shape: [8, 4, 256]`

✅ So the final 3D tensor fed into the Transformer model has:
> **8 batches × 4 tokens per sequence × 256 embedding dimensions**

This 3D structure is what the Transformer processes in its attention layers.

`In **CODE**:`
```python
from importlib import metadata
import tiktoken # GPT 2 tokenizer.
import torch # pyhon deep learning framework.
from torch.utils.data import Dataset, DataLoader # this library have these pytorch base classes for creating datsets.
# Dataset → Defines how data is stored and accessed.
# DataLoader → Defines how data is batched, shuffled, and fed into your model.

class GPTDatasetV1(Dataset): # in brackets means this class GPTDatasetV1 is inheriting from other class Dataset.
    def __init__(self, txt, tokenizer, max_length, stride): 
        # max_length - how long each training sequence should be.
        # stride - how far to move the sliding window beween chunks. (controls overlap)
        self.input_ids = []
        self.target_ids = [] # two arrays initialised first.

        # Tokenize the entire text
        token_ids = tokenizer.encode(txt, allowed_special={"<|endoftext|>"})
        # tokenizer is object, enocode is method in tiktoken library but first tokenizer is initialized downside.

        # Use a sliding window to chunk the book into overlapping sequences of max_length
        for i in range(0, len(token_ids) - max_length, stride): 
            # in this for stop we're taking this len(token_ids) - max_length because if we take len(token_ids) the slice 
            # i+max_length would go beyond the end of the list -- causing an error, so we stop at this (len(token_ids) - max_length)
            input_chunk = token_ids[i:i + max_length]
            target_chunk = token_ids[i + 1: i + max_length + 1]
            self.input_ids.append(torch.tensor(input_chunk))
            self.target_ids.append(torch.tensor(target_chunk))

    def __len__(self): # this method tells PyTorch how many samples are present in your dataset.
        return len(self.input_ids)

    def __getitem__(self, idx): # when you ask for one training eg (datset[i]), it returns a pair that is 
        # (input_tokens, target_tokens)
        return self.input_ids[idx], self.target_ids[idx]
    

def create_dataloader_v1(txt, batch_size=4 #it is how many CPU processors you wanna run parallely
                         , max_length=256, 
                         stride=128, shuffle=True, drop_last=True,
                         num_workers=0 # number of CPU threads which we wanna run simultaneously 
                         ):

    # Initialize the tokenizer
    tokenizer = tiktoken.get_encoding("gpt2") # this loads the same tokeniaer used by GPT-2 model.


    # Create dataset
    dataset = GPTDatasetV1(txt, tokenizer, max_length, stride)

    # Create dataloader
    dataloader = DataLoader(
        dataset, #dataloader will just look for __getitem__ in class and will return the input and the target pairs.
        batch_size=batch_size,
        shuffle=shuffle,
        drop_last=drop_last,
        num_workers=num_workers
    )

    return dataloader

with open("the-verdict.txt", "r", encoding="utf-8") as f:
    raw_text = f.read()


vocab_size = 50257 # no. of token ids
output_dim = 256 # no. of dimensions.

token_embedding_layer = torch.nn.Embedding(vocab_size, output_dim)

max_length = 4
dataloader = create_dataloader_v1(
    raw_text, batch_size=8, max_length=max_length,
    stride=max_length, shuffle=False
)
data_iter = iter(dataloader)
inputs, targets = next(data_iter)
print("Token IDs:\n", inputs)
print("\nInputs shape:\n", inputs.shape)

token_embeddings = token_embedding_layer(inputs)
print(token_embeddings.shape)

context_length = max_length
pos_embedding_layer = torch.nn.Embedding(context_length, output_dim)

pos_embeddings = pos_embedding_layer(torch.arange(max_length))
print(pos_embeddings.shape)

input_embeddings = token_embeddings + pos_embeddings
print(input_embeddings.shape)
```

---


