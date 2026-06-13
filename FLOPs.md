**FLOPs : **

FLOPs stand for floating point operations, metric used to count individual calculations, specifically additions and multiplications, that involve decimal numbers
  - single FLOP : if an ai model calculates a * b + c using decimal numbers, it has performed roughly 2 FLOPs
  - FLOPS : floating point operations per second, measures the raw speed and capability of a computer chip
  - Scale of AI : deep learning requires so much math that engineers measure chip performance in massive scales : 
              - TeraFLOPS : trillions of operations per second
              - PetaFLOPS : quadrilliions of operations per second

Why FLOPs matter to AI : training models like chatgpt requires septiliions of mathematical ops, if a chip does not have a high flops rating, training an llm model would take decades instead of days

**Normal chips vs Powerful AI chips : **
difference between any normal computer chip (CPU) and powerful ai chip (GPU or TPU) is not just that AI chips are faster, they are built with entirely different physical architcetures to solve different types of problems

| Feature [1, 2, 3, 4, 5, 6, 7] | Normal Chips (CPUs) | Powerful AI Chips (GPUs/TPUs) |
| Analogy | A team of 4 to 8 Brilliant Mathematicians. | A stadium filled with 10,000 Kindergarteners. |
| Core Count | Very few cores (usually 4 to 16). | Thousands of small cores (often 5,000 to 15,000+). |
| Processing Style | Sequential: Solves one complex problem at a time, incredibly fast. | Parallel: Solves thousands of tiny, simple math problems simultaneously. |
| Specialization | General Purpose: Can run operating systems, handle user clicks, and jump between tasks. | Matrix Math: Hyper-specialized in multiplying massive grids of decimal numbers. |
| Memory Setup | Standard RAM (optimized to fetch varied data points quickly). | High-Bandwidth Memory (HBM/VRAM) to stream massive streams of data smoothly. |


Visual difference : if a cpu is given a matrix multiplication task (core of dl) it uses its few powerful cores to multiply the numbers one by one, creating a massive traffic jam,   --- while if we give an ai chip a matrix multiplication task, assigns every one core to every single number in the grid, computes the entire math prob in a single, unified pulse.


**WHAT IS MACHINE LEARNING : **
branch of ai that gives computers ability to learn from data without being explicitly programmed to do so, instead of a human writing strict rules, machien analyzes data to discover patterns and create its own rules

3 main types of ml : 
- supervised learning : model uses labelled data, **input data paired with the correct ans **to help with prediction evaluation
- Unsupervised learning : model analyzes unlabelled data to find hidden structures or groupings on its own , for eg : grouping ecommerce customers into clusters based on purchasing habits
- Reinforcement learning : model learns by trial and error within an environment to maximise a reward, for eg : teaching an ai agent to play chess or navigate a virtual maze

**how differs from traditional programming : **
- traditional prog : feed the computer data + rules -> outputs the answers
- machine learning : you feed the computer data + answers -> outputs the rules (trained model) 

ML VS DL : ml relies heavily on human engineers to manually clean data and select relevant features (eg, telling the computer to look at specific pixel edges to dientify a car) , works well on smaller structured data like spreadsheets.


WHAT IS NLP? 
is a branch of artificial intelligence that gives computers the ability to understand interpret and generate human language. It bridges the gap between human communication (which is messy, nuanced and unstructured) and computer code (which relies on strict numbers and rules).

**core challenged nlp solves : **human lang highly complex for comps because 
- ambiguity : words can have multiple meanings based on context
- sarcasm and tone : sentences lke oh great a flat tyre,  requires emotional context to understand
- syntax and slang : grammatical rules constantly change and new cultural slang emerges daily

**How NLP Processes text (the traditional pipeline) : **
 before an ai model undertsnad a sentence, raw text must be broken down into pieces a comp can calculate

raw text -> tokenization -> lemmatization -> vectorizatio -> ai model

**- Tokenization** : splitting continuous sentence into individual units or words
**- Stop word removal** : filtering out common words that carry little unique meaning such as "and", "the" and "is".
**- Lemmatization & Stemming : **reducing words to their base or dictionary form (running, ran runs all contract down to the word run)
**- Vectorization (embeddings) : **converting the porcessed words into arrays of decimal numbers, because computer chips can only process mathematical equations

Everyday egs of nlp :  
- search engines - googl eundertsanding the true intent behind a messy search query rather than just matching exact keywords
- sentiment analysis - software anakyzing thousands of customer reviews to automatically classify them as positive, negative or neutral
- machine translation : instantly translating text between different languages
- voice assistants : siri alexa assistant, turning spoken voice to text, figuring out intent and responsidng back to you

**evolution of nlp to llms : **
- trad nlp : relied heavily on hard coded grammar rules and statistical probabs of words appearing next to each other
- Modern NLP (deep learning) : uses the transformer architecture, instead of reading words one by one, transformers look at entire sentences simultaneously to understand how every single word relates to every other word, this specific breakthrough is what allowed simple NLP to scale up into modern llms


**VECTORIZATION : **
process of converting non numerical data - like words, sentences or images into arrays of decimal numbers called vectors

computer chips, graphic cards and NNs can not read text, see pixels or listen to audio dircetly, they only undertsand math ops like + *, vectorization is the crucial bridge that turns human data into mathematical formats that ai hardware can compute

**how text vectprization works : **
- when text is vectorized, transformed into a list of numbers, 2 primaary ways to do this,, ranging from simple to advanced
        - **one hot encoding (trad method**) : bag of words, simply maps words into static vocabulary checklist, for apple banana cat in our vocabulary, it gives apple as 001, banana as 010, where apply and banana have no mathematical relationship
        - **modern method (dense embeddings (semantic vectors)) : **modern deep learning models place words into a multi dimensional mathematical space (often 768 to 1536 dimensions deep) 
                      - words with similar meanings are given similar numerical values, ensures they sit close to each other inside the computer's memory space
                      - Vector("King") - Vector("Man") + Vector("Woman") = Vector("Queen")
                      - as numbers match real world concepts, model understand that puppy and dog are deeply related, even tho they are spelled completely differently

Everything is a vector space, and the number of dimensions, depends on the number of features, which can be a lot due to which 768 & 1536.







 




