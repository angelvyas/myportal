---
title: 'LLM Data Preprocessing'
date: 2025-11-08
draft:  false
featured: false  
description: "LLM - Data Preprocessing"
thumbnail: "/posts/LLM/images/pre.png"
featureImage: "/posts/LLM/images/pre.png" 
shareImage: "/posts/LLM/images/pre.png"
author: "Angel Vyas"
tags:
    - llm
categories:     
    - llm
---

# LLM Data Preprocessing

Preprocessing text data is one of the most important steps in training Large Language Models (LLMs).  
The first step in this process is **tokenization** — the act of converting raw text into smaller, manageable units called *tokens*.
</br>

## 1. Tokenization

Tokenization can be broadly categorized into three types:

1. **Word-based Tokenization**  
2. **Subword-based Tokenization**  
3. **Character-based Tokenization**

In this section, we start with **word-based tokenization**.

---

### 1. Word-based Tokenization

Word-based tokenizers split text into tokens at word boundaries.  
For example:


"This is an example"


would be tokenized into:
```python
["This", "is", "an", "example"]
```

Then, each word (token) is assigned a unique numerical ID.

```python
[0, 1, 2, 3]
```

A simple implementation of a word-based tokenizer in Python can look like this:

```python
import re
with open("the-verdict.txt", "r", encoding="utf-8") as f: #encoding is used to include special characters while reading the file.
    raw_text = f.read()
    
print("Total number of character:", len(raw_text))
print(raw_text[:99])

preprocessed = re.split(r'([,.:;?_!"()\']|--|\s)', raw_text)
preprocessed = [item.strip() for item in preprocessed if item.strip()] #item.strip() removes extra space from both the sides, and if item..stip() is empty it remove it.


print(preprocessed[:30])
print(len(preprocessed))

all_words = sorted(set(preprocessed))#firt set functions keeps only unique words from preprocessed then sorted function sorts the file into alphabatical order.
vocab_size = len(all_words) #counts unique words.

print(vocab_size)

vocab = {token:integer for integer,token in enumerate(all_words)} #enumerate give word a number automatically.
for i, item in enumerate(vocab.items()):# .items() is a dictionary method (function) that returns all key-value pairs of the dictionary.
    print(item)
    if i >= 50:
        break





class SimpleTokenizerV1:
    def __init__(self, vocab):#it initializes the tokenizer with a given vocabulary.
        #vocab = {'Hello': 0, 'world': 1, '.': 2}
        #tokenizer = SimpleTokenizerV1(vocab)

        self.str_to_int = vocab
        self.int_to_str = {i:s for s,i in vocab.items()}
    
    def encode(self, text):
        preprocessed = re.split(r'([,.:;?_!"()\']|--|\s)', text)
                                
        preprocessed = [
            item.strip() for item in preprocessed if item.strip()
        ]
        ids = [self.str_to_int[s] for s in preprocessed] #For every token s in the list preprocessed, get its corresponding integer ID from the dictionary self.str_to_int
        return ids
        
    def decode(self, ids):
        text = " ".join([self.int_to_str[i] for i in ids]) #join is used to join the individual tokens.      
        # Replace spaces before the specified punctuations
        text = re.sub(r'\s+([,.?!"()\'])', r'\1', text)
        return text
    
tokenizer = SimpleTokenizerV1(vocab)
text = """"It's the last he painted, you know," 
           Mrs. Gisburn said with pardonable pride."""
ids = tokenizer.encode(text)
print(ids)
```
### Limitations of Word-based Tokenization

Word-based tokenization, though simple and intuitive, has several key drawbacks:

1. **Out-of-Vocabulary (OOV) Words**  
   - Any word not present in the tokenizer’s vocabulary during training cannot be processed later.  
   - For example, if the tokenizer was trained on `"this is an example"` and encounters `"this is new"`, the word `"new"` will cause an error.  
   - This makes handling unseen or rare words difficult without expanding the vocabulary.

2. **No Semantic Relationship Between Token IDs**  
   - Token IDs are assigned arbitrarily and do not reflect meaning.  
   - Words like `"happy"` and `"joyful"` may have IDs that are far apart even though they are semantically similar.  
   - This shows that token IDs themselves carry no sense of similarity — embeddings are needed later to capture that.

Because of these issues, modern LLMs have moved toward **subword tokenization** methods (like **BPE** or **SentencePiece**) that can represent new words more flexibly and reduce vocabulary size.


### **Handling Missing Words**

If we try to encode a sentence containing a word not present in the vocabulary, such as:

tokenizer.encode("this is new")


we’ll get a `KeyError`, since "new" is `not part of the vocabulary`.

This highlights the need to consider `large and diverse training datasets` when building vocabularies for LLMs — ensuring that the vocabulary covers as many words and variations as possible.
A small or biased dataset can cause many unseen words to be missing during inference.

### Adding Special Context Tokens

In real-world LLM training, special tokens are added to mark specific positions or meanings within text sequences.
These tokens provide context, structure, and consistency to the input text.

Some of the most common special tokens include:

`<|unk|>` – Represents an unknown word not found in the vocabulary.

`<|endoftext|>` – Indicates the end of a text segment.

`<bos>` – Marks the beginning of a sequence.

`<eos>` – Marks the end of a sequence.

`<pad>` – Used for padding, so that all sequences in a batch have the same length.

These special tokens help models understand when text starts or ends, when a word is missing, and how to handle text sequences during batch training.

 ### **Note:**
GPT-style models simplify this process for efficiency.

- They only use the `<|endoftext|>` token to mark the end of a sequence.
- GPT models do not use `<|unk|>`, `<bos>`, `<eos>`, or `<pad>` tokens.
- Instead of relying on unknown tokens, GPT uses a `Byte Pair Encoding (BPE) tokenizer`, which breaks down words into smaller subword units.

This allows GPT to represent any word — even new or rare ones — as a combination of known subword tokens.

---
## 2. Character-based Tokenization

Character-based tokenization breaks text into **individual characters** instead of words or subwords.  
Each character — including letters, punctuation marks, and spaces — is treated as a separate token.


### Example

Let’s take a simple sentence:

"this is an example"

Character-based tokenization would split it as:

```python
["t", "h", "i", "s", " ", "i", "s", " ", "a", "n", " ", "e", "x", "a", "m", "p", "l", "e"]
```
Every single character, including spaces, becomes a token.

### **Advantages**

1. Very Small Vocabulary Size

- The vocabulary is limited to all possible characters (e.g., letters, digits, punctuation).
- This makes it much smaller and easier to manage compared to word-level vocabularies.

2. No Out-of-Vocabulary (OOV) Problem

- Since all words are made up of characters, even unseen or rare words can be represented easily.
- For example, if a new word "xylophone" appears, it can still be tokenized as individual characters.

### **Limitations**

1. Loss of Word-level Meaning

- Characters on their own don’t carry semantic meaning.
- The model must learn how sequences of characters form words and meanings, which makes training more difficult.

2. Much Longer Token Sequences

- A single word like "example" becomes 7 tokens instead of one.
- This increases input length significantly and slows down training and inference.

Because of these issues, character-based tokenization is rarely used in large-scale language models on its own.
However, its principles are valuable and are partially incorporated into subword-based tokenization, which aims to combine the best of both worlds — smaller vocabularies and meaningful units.

---
    
## 3. Subword-based Tokenization

Subword-based tokenization is a technique designed to find a balance between **word-based** and **character-based** tokenization.  
It divides text into units that are **smaller than words** but **larger than individual characters** — such as common prefixes, roots, or suffixes.  
This approach helps models efficiently handle both frequent and rare words.



### Rules of Subword Tokenization

1. **Do Not Split Frequently Used Words**  
   - Common words that appear often in the dataset (like `the`, `you`, or `computer`) are kept as single tokens.  
   - Keeping them intact makes processing faster and avoids unnecessary fragmentation.

2. **Split Rare Words into Smaller Subwords**  
   - Words that appear rarely or are unseen are split into smaller, meaningful parts (subwords).  
   - This allows the model to represent new words using familiar components.

For example:

| Word  | Subword Tokens |
|--------|----------------|
| boy    | ["boy"]        |
| boys   | ["boy", "s"]   |

Here, the model learns that **“boy”** is a root word and **“s”** is a suffix added to make it plural.  
If a new word like `"boyish"` appears, it can still be tokenized as:

```
["boy", "ish"]
```

Even if `"boyish"` was never seen during training, the model can still understand it using existing subword units.


### Advantages
1. **Helps the Model Learn Word Relationships**  
   - By breaking words into reusable parts, the model can generalize better across related words.  
   - For example, from `"play"` → `"playing"`, `"played"`, `"player"`, the model learns that these share the same root **“play”**.

2. **Captures Morphological Patterns**  
   - The model also learns how different words share similar suffixes or prefixes.  
   - For example, `"tokenization"` and `"modernization"` share the suffix **“ization”**, helping the model understand that both describe processes or actions.

3. **Reduces Vocabulary Size and Avoids OOV Problems**  
   - Since any new or rare word can be represented as a combination of known subwords, there’s no true “unknown” word problem.  
   - This makes subword tokenization ideal for large-scale language models.



> **In summary:**  
> Subword-based tokenization allows LLMs to represent both common and rare words efficiently.  
> It helps the model learn **morphological structure**, reduces **vocabulary size**, and eliminates **out-of-vocabulary** issues — making it the foundation of tokenization in modern architectures like GPT, BERT, and T5.

---

## Byte Pair Encoding (BPE)

**Byte Pair Encoding (BPE)** is one of the most popular algorithms used for **subword-based tokenization** in modern Large Language Models (LLMs).  
It efficiently compresses text by merging the most frequent pairs of symbols (starting from individual characters) into new subword tokens.

BPE strikes a balance between word-level and character-level tokenization — keeping frequent patterns together while splitting rare ones.


### Example: Step-by-Step BPE Process

Let’s start with a small example to understand how BPE works.

#### Original data:
```
aaabdaaabac
```

At the beginning, each character is treated as a separate token:

```
["a", "a", "a", "b", "d", "a", "a", "a", "b", "a", "c"]
```

#### Step 1: Count symbol pairs
We count all adjacent pairs of symbols:

| Pair | Frequency |
|------|------------|
| a a  | 5          |
| a b  | 2          |
| b d  | 1          |
| d a  | 1          |
| b a  | 2          |
| a c  | 1          |

The most frequent pair is **`a a`**, which occurs 5 times.

#### Step 2: Merge the most frequent pair
We replace all occurrences of `a a` with a new symbol, say **`z`**:

```
a a → z
```

So the new sequence becomes:

```
["z", "a", "b", "d", "z", "b", "a", "c"]
```

#### Step 3: Repeat the process
Now we again count the most frequent pairs:

| Pair | Frequency |
|------|------------|
| z a  | 2          |
| a b  | 1          |
| b d  | 1          |
| d z  | 1          |
| z b  | 1          |
| b a  | 1          |

The most frequent pair is **`z a`**, so we replace it with a new symbol **`y`**:

```
z a → y
```

Resulting sequence:
```
["y", "b", "d", "y", "b", "a", "c"]
```

If we continue merging the most frequent pairs step by step, we eventually form a vocabulary of subword units that represent the data compactly.

---

### How BPE is Used in LLMs

In LLMs, BPE is used to tokenize massive amounts of text efficiently.  
Here’s how it works conceptually:

1. **Training Phase**
   - The tokenizer starts with all unique characters in the corpus.
   - It repeatedly merges the most frequent pairs to form new subwords.
   - This process continues until a predefined vocabulary size is reached (e.g., 50,000 tokens).

2. **Tokenization Phase**
   - During tokenization, new text is broken into the longest possible subwords found in the vocabulary.
   - Unseen words are automatically split into smaller known parts, eliminating the out-of-vocabulary problem.

---
### Advantages of Byte Pair Encoding (BPE)

BPE offers several advantages that make it ideal for **modern LLMs** like GPT:

1. **Eliminates Out-of-Vocabulary (OOV) Issues**  
   - Since any new or rare word can be represented as a combination of existing subword units, the model never encounters truly “unknown” words.  
   - For example, `"newest"` can be tokenized as `["new", "est</w>"]` even if it never appeared in training.

2. **Keeps Vocabulary Size Manageable**  
   - BPE allows a fixed vocabulary size (for example, 50,000 tokens in GPT models).  
   - This ensures efficient storage and computation while still covering almost all possible text combinations.

3. **Retains Root Word Meanings**  
   - By merging frequent subword patterns, BPE preserves meaningful components like roots and suffixes.  
   - For instance, words like `"old"`, `"older"`, and `"oldest"` share the common root **“old”**, allowing the model to learn relationships between them.  
   - This helps LLMs generalize across similar word forms and better understand morphology.

4. **Efficient and Scalable for Large Corpora**  
   - The iterative merging process scales well for large datasets and languages with rich morphology.  
   - It’s computationally simple and yields robust, reusable subword vocabularies.

---

### Important Observation in BPE Implementation

In GPT-style tokenizers, a few implementation details are noteworthy:

- The **special token `<|endoftext|>`** is used to indicate the end of a text sequence.  
- This token is typically assigned one of the **largest token IDs** in the vocabulary to keep it unique and easily distinguishable from normal text tokens.  
- GPT models **do not use** tokens like `<unk>`, `<bos>`, or `<eos>` — only `<|endoftext|>` is reserved for simplicity and consistency.


### Python Implementation of BPE
```python
from importlib import metadata
import tiktoken

print("tiktoken version:", metadata.version("tiktoken"))
tokenizer = tiktoken.get_encoding("gpt2") # we can instantiate the bpe tokenizer from tiktoken as this.
# the use of this object tokenizer (instance to tiktoken library), is similar to that of my_token.py that we have done before.
text = (
    "Hello, do you like tea? <|endoftext|> In the sunlit terraces"
     "of someunknownPlace." # in output someunknownPlace is broken down into sub-words then token ids are assigned.
)

integers = tokenizer.encode(text, allowed_special={"<|endoftext|>"})

print(integers)
strings = tokenizer.decode(integers)

print(strings)
integers = tokenizer.encode("Akwirw ier")
print(integers)

strings = tokenizer.decode(integers)
print(strings)
```
</br>

---


## Creating Input–Target Pairs

After tokenization, the next essential preprocessing step before generating embeddings is **creating input–target pairs**.  
This process transforms a tokenized sequence into a supervised-like format, allowing the model to learn language structure through **next-token prediction**.



### Learning Type: Self-Supervised / Autoregressive Learning

Even though we generate input–target pairs, this task is **not truly supervised** — no external labels are provided.  
Instead, the model learns directly from the text itself.  

This setup is known as **self-supervised learning**, and in the specific case of predicting the next token, it is called **autoregressive training**.

- **Self-supervised:** The targets come from the data itself.  
- **Autoregressive:** The model predicts the next token based on previous tokens.



### How It Works

Let’s take a tokenized example:

```
["this", "is", "an", "example"]
```

We want the model to predict the next token for every position.  
So we create input–target pairs like this:

| Input Sequence         | Target Token |
|-------------------------|---------------|
| ["this"]                | "is"          |
| ["this", "is"]          | "an"          |
| ["this", "is", "an"]    | "example"     |

Each time, the model only sees the **past** tokens and tries to predict the **next** one.  
During training, all words **beyond the target** are **masked out** so the model cannot peek into the future.



### Implementing Input–Target Pair Creation

In practice, this step is often implemented via a **data loader**, which dynamically generates training examples from long token sequences.

A **data loader**:
- Reads long tokenized sequences.
- Uses a **sliding window** approach to create smaller, fixed-length chunks.
- For each chunk, it prepares:
  - An **input** sequence (all tokens except the last one).
  - A **target** sequence (all tokens except the first one).



### Example of a Sliding Window Approach

Suppose we have this tokenized sequence of IDs:

```
[10, 11, 12, 13, 14, 15]
```

Let’s assume:
- **Window size = 4**
- **Stride = 2**

The loader will produce overlapping sequences:

| Window | Input Tokens  | Target Tokens |
|---------|----------------|----------------|
| 1       | [10, 11, 12]   | [11, 12, 13]   |
| 2       | [12, 13, 14]   | [13, 14, 15]   |

Here:
- The **stride** (2) controls how far we move the window for the next batch.
- Smaller stride → more overlap and more training examples.
- Larger stride → less overlap and faster training.


### Understanding Key Parameters

- **Window Size (Context Length):**  
  The number of tokens the model can “see” at once.  
  For example, GPT models might use a context window of 1024 or even 8192 tokens.

- **Stride:**  
  Determines how much the window shifts for each new input.  
  Example: With stride 2 and window 4, `[1,2,3,4]` → `[3,4,5,6]`.

- **Batch Size:**  
  The number of samples processed together in one forward/backward pass.  
  A larger batch size improves training stability but requires more memory.



### Example: Implementing a Simple Data Loader in Python

```python
from importlib import metadata
import tiktoken
import torch
from torch.utils.data import Dataset, DataLoader # this library have these pytorch base classes for creating datsets.

class GPTDatasetV1(Dataset):
    def __init__(self, txt, tokenizer, max_length, stride): 
        # max_length - how long each training sequence should be.
        # stride - how far to move the sliding window beween chunks. (controls overlap)
        self.input_ids = []
        self.target_ids = [] # two arrays initialised first.

        # Tokenize the entire text
        token_ids = tokenizer.encode(txt, allowed_special={"<|endoftext|>"})

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

import torch
print("PyTorch version:", torch.__version__)
dataloader = create_dataloader_v1(
    raw_text, batch_size=1, max_length=4, stride=1, shuffle=False
)

data_iter = iter(dataloader)
first_batch = next(data_iter)
print(first_batch) # first batch means the input and the output tensor.

second_batch = next(data_iter)
print(second_batch)

dataloader = create_dataloader_v1(raw_text, batch_size=8, max_length=4, stride=4, shuffle=False)

data_iter = iter(dataloader)
inputs, targets = next(data_iter)
print("Inputs:\n", inputs)
print("\nTargets:\n", targets)
```



### Summary

- **Creating input–target pairs** is the final step before embedding generation.  
- It converts raw token sequences into training-ready data for autoregressive learning.  
- The **data loader** efficiently generates overlapping context–target pairs using parameters like **window size**, **stride**, and **batch size**.  
- This step ensures the model learns to predict the next token — the core objective of LLM pretraining.
