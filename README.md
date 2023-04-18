# Amazon Comprehend in detecting creative works titles

## Introduction
[Amazon Comprehend](https://aws.amazon.com/comprehend/) is a natural language processing (NLP) service provided by Amazon Web Services (AWS) that makes it easy for developers to add NLP capabilities to their applications. Comprehend can analyze text in multiple languages and extract valuable insights such as sentiment analysis, entity recognition, topic modeling, and more. This service is particularly useful for businesses looking to better understand their customers, analyze feedback, and gain actionable insights from large volumes of text data.

As noted by AWS in their [documentation](https://docs.aws.amazon.com/comprehend/index.html), "the service can identify mentions of movies, books, music albums, and television shows in the text, even if the titles are misspelled or abbreviated." In this project, we evaluate Amazon Comprehend's accuracy and usefulness in detecting creative works titles (books, song names, movies titles,etc) given a text input.

## What is Named Entity Recognition?
Named Entity Recognition (NER) is a NLP subtask that involves identifying and classifying named entities in text into predefined categories, such as organizations, locations and titles. Machine learning models are trained on annotated datasets to extract the entities and predict the labels. NER has a wide range of real-world applications, such as information extraction and content recommendation. Check this notebook by Professor Choi from Emory University for more information.

## Why Titles of Creative Works are especially interesting?
Detecting creative works titles using natural language processing (NLP) can be a challenging task due to several factors. 
1. Language ambiguity leads to multiple possible interpretations of a given phrase. For example, the phrase "The Crown" could refer to the Netflix series or the headwear worn by royalty. 
2. Misspellings and variations in titles names such as abbreviations or nicknames can make it difficult for NLP algorithms to accurately identify them. 
3. Common words or phrases contained in titles that may not be unique to the creative work in question can make it difficult for the algorithm to differentiate them.
4. Context plays a significant role in determining whether a given phrase refers to a creative work title or not, and NLP algorithms may struggle to accurately interpret contextual cues.

In the literature, titles of creative works (movie/book/song/software names) are complex named entities (NE) and pose special challenges for named entity recognition (Ashwini and Choi, 2014). These entities can be linguistically complex, emerging, and written informally on on social media. Dealing with complex and ambiguous entities in open domain environments is a challenging NLP task (Meng et al., 2021). Researchers using NER on downstream tasks have also noted that a significant proportion of their errors are due to NER systems failing to recognize complex entities (Luken et al., 2018; Hanselowski et al., 2018).

More intuitively, let's look at the following examples to see why recognizing titles of creative works is challenging.

The Great Gatsby: the "conventional" named entity; a adjective followed by noun.

To Kill a Mockingbird: infinitives

Dial M for Murder: imperative clause

1984: a number

Yours Truly: this book is released in April 2023, which means you, and the model, possibly have not seen it before.
## Hypothesis and Significance
Based on the literature, we propose the following hypothesis: When recognizing titles of creative works, the performance of Amazon Comprehend is significantly influenced by capitalization, conventionality of the title’s linguistics constitute, and titles spelling.

## The significance of the project
The titles of creative works are linguistically complex, innovative, and emerging. The titles can be colloquial or be mentioned in a colloquial setting like social media. They can be gerunds and infinitives rather than traditional noun phrases. New works are released every day. If the performance of Amazon Comprehend is significantly influenced by capitalization, conventionality of the title’s linguistics constitute, and the released date to recognize these titles, its accuracy and robustness will be limited. After people recognize these limitations and further train Amazon Comprehend, its robustness in an open-world setting can be improved.

## Dataset Description
### Data Collection
We use the English Dataset from [MultiCoNER Datasets](https://registry.opendata.aws/multiconer/), a large multilingual dataset for Named Entity Recognition. This dataset is designed to represent contemporary challenges in NER, including low-context scenarios (short and uncased text) and syntactically complex entities like movie titles (Malmasi et al., 2022). It is a 26M token dataset compiled from public resources and contains 36 NE classes. The dataset is the registry of open data on AWS and is managed by Amazon. (add the pie chart here)

### Data Quality
The researchers evaluated the NER label quality of the dataset. They generated a small random sample of 400 sentences, and assessed the accuracy of NER gold labels, which was measured at 94% accuracy for the english dataset (Malmasi et al., 2022).

### Data Collection


## Data Analysis and Visualization


## Data Architecture


## Resources and Acknowledgements
Malmasi, Shervin, et al. 2022. Semeval-2022 Task 11: Multilingual Complex Named Entity Recognition (Multiconer). Proceedings of the 16th International Workshop on Semantic Evaluation (SemEval-2022).

Tao Meng, Anjie Fang, Oleg Rokhlenko, and Shervin Malmasi. 2021. GEMNET: Effective gated gazetteer representations for recognizing complex entities in low-context input. In Proceedings of the 2021 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies, pages 1499–1512.

Sandeep Ashwini and Jinho D Choi. 2014. Targetable named entity recognition in social media. arXiv eprints, pages arXiv–1408.

Shervin Malmasi, Anjie Fang, Besnik Fetahu, Sudipta Kar and Oleg Rokhlenko. 2022. MultiCoNER: a Large-scale Multilingual dataset for Complex Named Entity Recognition. Jackson Luken, Nanjiang Jiang, and Marie-Catherine de Marneffe. 2018. QED: A fact verification system for the FEVER shared task. In Proceedings of the First Workshop on Fact Extraction and VERification (FEVER), pages 156–160, Brussels, Belgium. Association for Computational Linguistics.

Jacob Devlin, Ming-Wei Chang, Kenton Lee, and Kristina Toutanova. 2019. BERT: pre-training of deep bidirectional transformers for language understanding. In NAACL-HLT (1). Association for Computational Linguistics.
