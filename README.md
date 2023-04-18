# Amazon Comprehend in detecting creative works titles

## Introduction
[Amazon Comprehend](https://aws.amazon.com/comprehend/) is a natural language processing (NLP) service provided by Amazon Web Services (AWS) that makes it easy for developers to add NLP capabilities to their applications. Comprehend can analyze text in multiple languages and extract valuable insights such as sentiment analysis, entity recognition, topic modeling, and more. This service is particularly useful for businesses looking to better understand their customers, analyze feedback, and gain actionable insights from large volumes of text data.

As noted by AWS in their [documentation] on Comprehend(https://docs.aws.amazon.com/comprehend/index.html), "the service can identify mentions of movies, books, music albums, and television shows in the text, even if the titles are misspelled or abbreviated." In this project, we evaluate Amazon Comprehend's accuracy and usefulness in detecting creative works titles (books, song names, movies titles,etc) given a text input.
## Challenges
Detecting creative works titles using natural language processing (NLP) can be a challenging task due to several factors. 
1. Language ambiguity leads to multiple possible interpretations of a given phrase. For example, the phrase "The Crown" could refer to the Netflix series or the headwear worn by royalty. 
2. Misspellings and variations in titles names such as abbreviations or nicknames can make it difficult for NLP algorithms to accurately identify them. (Example: Dial M for Murder)
3. Common words or phrases contained in titles that may not be unique to the creative work in question can make it difficult for the algorithm to differentiate them. (Example: Of Mice and Men)
4. Context plays a significant role in determining whether a given phrase refers to a creative work title or not, and NLP algorithms may struggle to accurately interpret contextual cues. (Example: 1984)
## Hidden variables
When recognizing titles of creative works, the performance of Amazon Comprehend is significantly influenced by capitalization, conventionality of the title’s linguistics constitute, and titles spelling. We will create different datasets catered to these features of texts and evaluate Amazon Comprehend on these inputs.

## Data Collection


## Data Analysis and Visualization


## Data Architecture


## Resources and Acknowledgements
