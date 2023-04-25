# Titles of Creative Works and Amazon Comprehend

If you hope to see the code and reproduce our results, you shall check [this blog](http://awscomprehend-walkthrough.s3-website.us-east-2.amazonaws.com/)!


## Introduction
[Amazon Comprehend](https://aws.amazon.com/comprehend/) is a natural language processing (NLP) service provided by Amazon Web Services (AWS) that makes it easy for developers to add NLP capabilities to their applications. Comprehend can analyze text in multiple languages and extract valuable insights such as sentiment analysis, entity recognition, topic modeling, and more. This service is particularly useful for businesses looking to better understand their customers, analyze feedback, and gain actionable insights from large volumes of text data.

As noted by AWS in their [documentation](https://docs.aws.amazon.com/comprehend/index.html), "the service can identify mentions of movies, books, music albums, and television shows in the text, even if the titles are misspelled or abbreviated." In this project, we evaluate Amazon Comprehend's accuracy and usefulness in detecting creative works titles (books, song names, movies titles,etc) given a text input.

![comprehend](https://user-images.githubusercontent.com/96922660/232936445-428f8cb1-26ce-4c67-8e5e-fb5118030294.png)


### What is Named Entity Recognition?
Named Entity Recognition (NER) is a NLP subtask that involves identifying and classifying named entities in text into predefined categories, such as organizations, locations and titles. Machine learning models are trained on annotated datasets to extract the entities and predict the labels. NER has a wide range of real-world applications, such as information extraction and content recommendation. Check this [notebook](https://github.com/emory-courses/computational-linguistics/blob/master/docs/named_entity_recognition.ipynb) by Professor Choi from Emory University for more information.

### Why Titles of Creative Works are especially interesting?
Detecting creative works titles using natural language processing (NLP) can be a challenging task due to several factors. 
1. Language ambiguity leads to multiple possible interpretations of a given phrase. For example, the phrase "The Crown" could refer to the Netflix series or the headwear worn by royalty. 
2. Misspellings and variations in titles names such as abbreviations or nicknames can make it difficult for NLP algorithms to accurately identify them. 
3. Common words or phrases contained in titles that may not be unique to the creative work in question can make it difficult for the algorithm to differentiate them.
4. Context plays a significant role in determining whether a given phrase refers to a creative work title or not, and NLP algorithms may struggle to accurately interpret contextual cues.

In the literature, titles of creative works (movie/book/song/software names) are complex named entities (NE) and pose special challenges for named entity recognition (Ashwini and Choi, 2014). These entities can be linguistically complex, emerging, and written informally on on social media. Dealing with complex and ambiguous entities in open domain environments is a challenging NLP task (Meng et al., 2021). Researchers using NER on downstream tasks have also noted that a significant proportion of their errors are due to NER systems failing to recognize complex entities (Luken et al., 2018; Hanselowski et al., 2018).

More intuitively, let's look at the following examples to see why recognizing titles of creative works is challenging.

- The Great Gatsby: the "conventional" named entity; a adjective followed by noun.

- To Kill a Mockingbird: infinitives

- Dial M for Murder: imperative clause

- 1984: a number

- Yours Truly: this book is released in April 2023, which means you, and the model, possibly have not seen it before.


## Hypothesis and Significance
Based on the literature, we propose the following hypothesis: **When recognizing titles of creative works, the performance of Amazon Comprehend is significantly influenced by capitalization, correct spelling, conventionality of the title’s linguistics constitute, and the popularity of the work.**
### The significance of the project
The titles of creative works are linguistically complex, innovative, and emerging. The titles can be colloquial or be mentioned in a colloquial setting like social media. They can be gerunds and infinitives rather than traditional noun phrases. New works are released every day. If the performance of Amazon Comprehend is significantly influenced by capitalization, conventionality of the title’s linguistics constitute, and the released date to recognize these titles, its accuracy and robustness will be limited. After people recognize these limitations and further train Amazon Comprehend, its robustness in an open-world setting can be improved.

###Tips for making your own investigation using the same method
- Look at our architecture first to have a intuitive and comprehensive understanding of the project.
- Our data extraction part is relatively complicated because the inital data format is complicated (designed for NER task in NLP). The goal is actually quite simple, we want sentences to be stored in list of tuple like this: [("sentence", has_title, "title), ("sentence", has_title, "title)]. You can create list of tuples from your own dataset in your way.
- For creating new categories and data analysis, you can just use our code if you data format is [("sentence", has_title, "title), ("sentence", has_title, "title)]. Remember to get your own google API Key. Note that Google Search API is not completely free, and you will be billed according to the API's pricing structure!
- You can also investigate your own hypothesis following our architecture. Possible topics include New Works vs. Old Works and English Works vs. Non-English Works.
- If you find any bugs in our project or find interesting results in your investigation, feel free to contact us!

## Our Architecture
<img width="949" alt="Screenshot 2023-04-18 at 10 59 50 PM" src="https://user-images.githubusercontent.com/91909405/232955823-57f3220c-3424-47a5-a671-95a0c40303fd.png">

## Dataset Description
### Data Collection
We use the English Dataset from [MultiCoNER Datasets](https://registry.opendata.aws/multiconer/), a large multilingual dataset for Named Entity Recognition. This dataset is designed to represent contemporary challenges in NER, including low-context scenarios (short and uncased text) and syntactically complex entities like movie titles (Malmasi et al., 2022). It is a 26M token dataset compiled from public resources and contains 36 NE classes. The dataset is the registry of open data on AWS and is managed by Amazon.

![Screen Shot 2023-04-18 at 8 24 13 PM](https://user-images.githubusercontent.com/96922660/232935221-f9cbc2f3-6190-4717-83cb-43bc7d0a1c3d.png)


### Data Quality
The researchers evaluated the NER label quality of the dataset. They generated a small random sample of 400 sentences, and assessed the accuracy of NER gold labels, which was measured at 94% accuracy for the english dataset (Malmasi et al., 2022).

## Data Preprocessing
There are two parts in dataset preprocessing: Data Extraction and New Categories Creation. In Data Extraction, we select samples related to titles of creative works and reformat the data. Our selected data has 16778 sentences. In New Categories Creation, we manipulate and transform the titles in dataset to new categories: Capitalized vs. Lowercase, Conventional vs. Unconventional, Correct vs. Misspelled and Popular vs. Unpopular.
### Data Extraction
For data extraction, we transform the data from the original format to [("sentence", has_title, "title), ("sentence", has_title, "title)]
More specifically, we follow these steps and implement it with the code below:

- extract entries from the dataset and concatenate words into sentence: lady in the dark – art direction : hans dreier and raoul pene du bois ; interior decoration : ray moyer

- label each entry as 0 - title included 1 - title absent

- put the formated data to a list

[(“He was succeeded as chancellor by sir frank kitto.”, 0, “”)'

(“I like reading The Great Gatsby.”, 1, “The Great Gatsby”)]

###Creating New Categories
We manipulate and transform the titles in dataset to new categories: Capitalized vs. Lowercase, Conventional vs. Unconventional, Correct vs. Misspelled and Popular vs. Unpopular.

####Capitalized vs. Lowercase
We lowercased the whole title to create the lowercased data.
Correct vs. Misspelled

#### Correct vs. Misspelled
We misspelled random character in the title with certain error rate to create the misspelled data.

#### Conventional vs. Unconventional
We define unconventional title as title that starts with verb, preposition, conjunction, WH-determiner, WH-pronoun, WH-possessive, WH-adverb, "to" as preposition or infinitive marker, existential there and list item marker. This definition is based on the literature in the background section.
We use nltk to perform POS Tagging.
#### Popular vs. Unpopular
To check the popularity of a creative work, we use the Google Search API. The number of results serve as an indicator of the work's popularity. We only processed ~100 samples because the limit of free Google Search API is 100 per day.

## Data Analysis and Visualization
We create a metric that extracts confidence scores from Amazon Comprehend for the recognized titles and multiply these confidence scores by a corresponding similarity score. The similary scores are determinted by the similarity between the recognized titles and the original titles. The more similar the comprehended titles are, the higher the similary score will be. In the end, the score represents how well Amazon comprehend performs.
We visualize them using different methods. Again, check [this blog](http://awscomprehend-walkthrough.s3-website.us-east-2.amazonaws.com/) for details!

## Conclusion
Based on our analysis, we have identified four previously unknown variables that impact the performance of Amazon Comprehend. By examining the performance score and recognition accuracy, we found that each of the four categories, namely capitalization, popularity, level of conventionality, and spelling accuracy, demonstrate significant differences in performance after implementing Amazon Comprehend. Even in the least siginificant group, misspelled versus correctly splelled titles, Amazon Comprend recognizes more than 3% titles on the correctly spelled titles. Thus, we can confirm that our hypothesis: When recognizing titles of creative works, the performance of Amazon Comprehend is significantly influenced by capitalization, correct spelling, conventionality of the title’s linguistics constitute, and the popularity of the work.

## Implications
For regular Amazon Comprehend users: If you want to have results with better accuracy, you can try to clean the data, making sure the titles are capitalized and correctly spelled. Also, you need to be catious on the titles that are linguistically complex and not that famous. They are more likely to be neglected by Amazon Comprehend.

For developers using or developers of Amazon Comprehend: The model's robustness and accuracy can be further improved. If Amazon Comprehend is trained on more noisy and colloquial data, it can have better ability to detect lowercased and misspelled titles. If Amazon Comprehend is trained on newer dataset that contains labels for creative works specifically, it will have better ability to extract creative titles with unconventional lingustics constitute. The developers can also find method in the open-world setting domain to help the model recognize unpopular/unseen/new works.
## Resources and Acknowledgements
Malmasi, Shervin, et al. 2022. Semeval-2022 Task 11: Multilingual Complex Named Entity Recognition (Multiconer). Proceedings of the 16th International Workshop on Semantic Evaluation (SemEval-2022).

Tao Meng, Anjie Fang, Oleg Rokhlenko, and Shervin Malmasi. 2021. GEMNET: Effective gated gazetteer representations for recognizing complex entities in low-context input. In Proceedings of the 2021 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies, pages 1499–1512.

Sandeep Ashwini and Jinho D Choi. 2014. Targetable named entity recognition in social media. arXiv eprints, pages arXiv–1408.

Shervin Malmasi, Anjie Fang, Besnik Fetahu, Sudipta Kar and Oleg Rokhlenko. 2022. MultiCoNER: a Large-scale Multilingual dataset for Complex Named Entity Recognition. Jackson Luken, Nanjiang Jiang, and Marie-Catherine de Marneffe. 2018. QED: A fact verification system for the FEVER shared task. In Proceedings of the First Workshop on Fact Extraction and VERification (FEVER), pages 156–160, Brussels, Belgium. Association for Computational Linguistics.

Jacob Devlin, Ming-Wei Chang, Kenton Lee, and Kristina Toutanova. 2019. BERT: pre-training of deep bidirectional transformers for language understanding. In NAACL-HLT (1). Association for Computational Linguistics.

We send colab notebook to our friends to test different parts of the project. Ellen recommends us to write tips for people making their investigations, and Gelin advises us to explain more on how to get Google Search API Key. We made the corresponding updates.

