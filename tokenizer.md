**TOKENIZER : **

tokenizer is the first step in allowing a machine to read and understand human language

**how does it work? : **at its simplest,, tokenizer is a tool that takes raw text and breaks it into smaller, manageable pieaces called tokens. Depending on the design, tokens might be words, subwords characters or even punctuation marks. By dividing text into smaller units, the tokenizer provides a structured representation that a lang model can work with. 

**What is a tokenizer in LLM ? : in llms** such as GPT, tokenization  does more than just splitting text, its mapped into unique numerical ID, creating a **sequence of numbers **that the model can process mathematically. Critical because neural networks cannot direvtlyread letters, they operate only on numbers. 

consider of tokens as lego blocks, each block represents a small defined piece of the whole, by snapping these blocks together in different ways, we can generate different new suntences or understand context. tokens **give ai the flexibility to interpret and generate a vast range fo human language.**

**HOW DOES A TOKENIZER WORK ? **

tokenizer takes raw textm breaks into smaller pieces, maps those into numerical IDs. (translation process, natural language in, machine readable code out)

DIFF **TYPES OF TOKENIZATION METHODS : **

- **word tokenization** : most straightforward, each word in sentence becomes a token, sometimes larger single words are broken down into smaller words. 
- **Character tokenization** : each character includign spaces and punctuation is treated as a token, AI as A and I. **avoids the problem of out of vocabulary words, but processing takes mcuh longer than word**
- **subword tokenization : **strikes a balance between words and characters, algos such as **Byte Pair Encoding (BPE), wordpiece and unigram language model** split text into chunks that are often whole words, but can also be meaningful fragments
- allows models to efficiently represent common words while handlign unusual terms by breaking them into smaller parts
**BERT AND GPT use **subword as core tokenizers.

 