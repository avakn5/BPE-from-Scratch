# A BPE (Byte Pair Encoding) Implementation from Scratch

Minimal Byte Pair Encoding (BPE) implementation from scratch [^1][^2], a subword tokenization algorithm used in modern large language models (LLMs).


Byte Pair Encoding is a subword tokenization algorithm originally adapted for NLP by [^2]. It works by iteratively replacing the most frequent pair of symbols in the text with a new symbol, effectively building a vocabulary. The following implementation includes extensive inline comments to aid understanding of the BPE implementation.

![Transformer Architecture](cs336_basics/figure/BPE_figure.jpeg)

### Repository Structure

```
cs336_basics/
│
├── bpe/                                # Byte-Pair Encoding (BPE) tokenizer
│   ├── __init__.py                    
│   ├── Pretokenization_example.py      
│   ├── Tokenizer_bpe.py                # BPE tokenizer implementation
│   └── Train_bpe.py                    # BPE training script
│
├── tests/                              # testing scripts
│
├── README.md                         
├── pyproject.toml                     # Metadata and dependencies
└── uv.lock                            # Lockfile for reproducibility
```

### Quick Start

Setup
```
bashgit clone https://github.com/avakn5/cs336_basics
pip install -e . && mkdir -p data && cd data
wget https://huggingface.co/datasets/roneneldan/TinyStories/resolve/main/TinyStoriesV2-GPT4-train.txt
```

Train the BPE Tokenizer
```
from cs336_basics.train_bpe import BPE

# Initialize BPE with special tokens
bpe = BPE(special_tokens=["<|endoftext|>"])

# Train on your text file
vocab, merges = bpe.train(
    input_path="data/tinystories_sample.txt",
    vocab_size=1000
)
```

Encode and Decode Text
```
tokenizer = BPE_Tokenizer(vocab, merges, special_tokens=["<|endoftext|>"])

# encoding/decoding
sample_text = "Once upon a time, there was a little robot who loved to code.<|endoftext|>"
encoded = tokenizer.encode(sample_text) # string ->token
decoded = tokenizer.decode(encoded) # token -> string
```

### STEPS to the BPE implementation: 

* 1- Pre-process the text.
* 2- Pretokenize the text.
* 3- UTF8 encode each pretoken.
* ------- Merging --------------
* 4- Split each pretoken into bytes.
* 5- count pair frequencies.
* 6- merge most frequent pairs.
* 7- repeat from step 4 until reached the vocab_size.

### Implemented Features:

* BPE training procedure.
* Encoder (text → token IDs).
* Decoder (token IDs → text).
* Passing all assignment tests:
&nbsp;BPE training: 3/3 tests passed
&nbsp; Tokenizer: 23/23 tests passed


[^1]: *Stanford CS336: Language Modeling from Scratch — Assignment 1 Instructions*. Stanford University, 2025. [https://stanford-cs336.github.io/spring2025/](https://stanford-cs336.github.io/spring2025/)  
[^2]: Sennrich, R., Haddow, B., & Birch, A. (2016). *Neural Machine Translation of Rare Words with Subword Units*. Proceedings of ACL. [https://arxiv.org/abs/1508.07909](https://arxiv.org/abs/1508.07909)
