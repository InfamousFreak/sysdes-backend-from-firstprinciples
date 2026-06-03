**ATTENTION IS ALL YOU NEED**

Input sequence : an ordered list of data points passed into a ml model where the specific position and context of each item matters

- order dependent : the seqwuence of same words but different rearrangement will mean somethign entirely different
- Variable length : can range from3 words to 500 paghe book
- contextually bound : meanign of any individual item (token )within the sequence heavily relies on the items that came before and after it

**Why the wordd "token" ?**

in comp sci, token is the smallest indivisible unit of data that holds meaningful value within a structure. Models do not process raw text, they require everythign to be chopped into pieces before assigning numeric IDs. are called tokens for several reasons : 
- tokens often smaller than words : tokenizers use algos like BPE to chop one word into more, so that the ai doesnt break when encounterign a type or a word it has never seen before
- punctuation and spaces are also tokens : also considered an independent piece of data with its own mathematical meaning, so tokens arent words, factually incorrect
- creates universality :  using the term token creates a universallanguage for data units, whether a model is looking for a syllabus of text, a picel patch of an image or chunk of audio, they treat that fundamental unit as a token

**Concept of input sequence belongs broadly to sequence modelling, spanning far beyond text.**



Bits per byte is a core information theoretic metric used to evaluate how accurately and efficiently a model predicts text. It measures the average number of binary bits required to compress or predict a single raw byte of UTF - 8 data. 

utf 8 data? : utf 8 data is text information stored using the utf 8 character encoding standard, which converts written letters, numbers and symbols into binary code that computers can understand. It stands for Unicode Transformation Format - 8 bit, and it is the dominant text format on the internet, powering 99% of all webpages as well as common data files like json and xml. 

- core features : universal compatibilty - UTF - 8 can represent virtually **every character from language **in the world. 
- **Variable width efficiency : doesnt** force every character to use same amount of memory, UTF - 8 uses a clever 1 to 4 byte flexible system, assigns fewer bytes to common characters and more bytes to complex symbols

- ASCII Backward compatibilty : The first 128 character of utf - 8 perfectly match ascii, this means any classic english text file is automatically a valid utf file

Flixibilty we talked about : 

**Character Type [1, 2, 3, 4, 5, 6]                Memory Used                    Examples **
Standard English & Numbers                    1 Byte (8 bits)                    A, b, 5, ? 
European & Middle Eastern Scripts        2 Bytes (16 bits)                é, ü, Ω, ç 
Asian Languages & Special Symbols      3 Bytes (24 bits)                語, हिं, €, → 
Emojis & Historic Scripts                           4 Bytes (32 bits)                😂, 𐤀 


