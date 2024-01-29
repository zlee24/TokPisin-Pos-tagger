# TokPisin-Pos-tagger
INTRODUCTION

This research project focuses on expanding natural language processing tools to encompass a broader range of languages, with a specific emphasis on marginalized languages like Tok Pisin. The primary objective is to create both a corpus and a Part of Speech (POS) tagger for Tok Pisin. POS tagging involves attaching grammatical categories, known as POS tags, to words. These tags enable word disambiguation based on contextual information, limiting potential interpretations. The development of an automatic POS tagger through the probabilistic training of a large number of POS disambiguations plays a vital rool in Natural Language Processing tools such as named entity recognition, word sense disambiguation, and a multitude of machine learning applications. 

Creating a corpus for Tok Pisin poses unique challenges, primarily due to the language's limited internet presence. Papua New Guinea's geographical and densely populated nature has hindered the growth of the national language on social media platforms and the availability of large data collections suitable for constructing natural language processing tools. While the Tok Pisin translation of the Christian Bible has been annotated and analyzed as a corpus, this study aims to incorporate a text that continually grows to capture the evolving language. To address this, the project focuses on scraping the archives of "Wantok Niuspepa," the only Tok Pisin newspaper in Papua New Guinea. This approach allows for a broader range of data points, diverse authorship, and insights into the formal word standardization prevalent in contemporary news articles.

TABLE OF CONTENTS

I. Link Scraper using pip requests

The first step is a link scraper using pip requests, which pulls all links from the archive website of the Wantok Niuspepa. However, there are extra links that are not pdf files, some broken links, and the pdf links we want are incomplete. We proceed to the next code to repair this.

II. Creating Complete Links using Python

In this step, the create_complete_links code, utilizing the Python, filters out non-PDF links from the text file generated in the previous step. This ensures that only the subdirectories holding the PDF files, which we want to scrape, remain. The code then completes the PDF links by adding the consistent scheme, subdomain, top-level domain, and second-level domain. The complete PDF links are written into another text file.

III. Token Strip and Count using Requests, BeautifulSoup, Collections, and Regular Expressions

Now that we have a text file of all the functional links, we are ready to scrape the data from each link. This step is an extended process with the full archive of links. If desired, manipulation of the link file can be done to gather a large amount of data, enough to work with neural methods, by using less than the over 600 links in the archives. The code goes through each page of each edition present in the links, finds all alphanumeric tokens, converts them to lowercase, and writes them to another text file while counting. Small manipulations via regular expressions can be quickly added to maintain punctuation, which is vital for some tasks, allowing the machine to find the sentence breaks.

IV. Creating a Gold Standard with Penn Tree Bank (PTB) Tagset

In this step, we switch to our linguist hats. The tokenized code is now used to create a gold standard for our training and test set. We implement the Penn Tree Bank (PTB) tagset on the data. The PTB consists of 36 tags, accounting for part of speech tags as well as other grammatical components such as case or tense. The Penn Tree Bank tagset offers a more in-depth analysis of the token compared to the Universal Dependency (UD) tagset. The Universal Dependency tagset is more constrained, offering a more general and practical approach to the part of speech tagset. The UD tagset consists of 17 tags, including an "other" category. It is important here to make reference to any dictionaries and consult primary (or more near primary) speakers, which increases the reliability of the grammatical judgments made. If working with a team of annotators, it is important to research a structure for the decision-making process to ensure the utmost accuracy of the tagged dataset.

V. CoNLL-U and UD Tagset using sys Library

Now that we have finished the important work of adding the PTB tags to the file, we are ready to further process the file into a machine-legible format for training. Additionally, we automate a process to assign the less informative UD tags based on the assigned PTB tag. Then, for each token with both PTB and UD tags assigned, the code will iterate through the tokens, pull the metadata (date of the issue, page number for the sentence token, and sentence ID for the overall collection of tokens), and display each token below with a plethora of columns of linguistic information that can be added. These tab-separated columns include ID, FORM, LEMMA, UPOS, XPOS, FEATS, HEAD, DEPREL, DEPS, and MISC. Our columns of interest will be ID, FORM, UPOS (UD tag), and XPOS (PTB tag). This format is legible for training UDPipe.

VI. Training the UDPipe Model

In this step, we train the UDPipe on the CoNLL-U file of doubly tagged tokens. The UDPipe will take the arguments "-tokenizer none -tagger none" as we have already gone through the process of tokenizing and tagging to our own specifications. The models argument for training is simply "-train", and once training is complete, the models argument for testing is "-tag". When training, the "SOMELANGUAGE" will be replaced with the language code of the language in reference, in our case, Tok Pisin. The input file will be the training CoNLL-U file with the appropriate tagsets. The training and testing processes can be easily automated to be performed one after another, especially for those interested in recording accuracy, precision, recall, and more. As always, keep in mind the data split when preparing for train and test. Divide the data near 80-20 or 80-10-10 if employing a dev set.

Usage and Further Development:

This project provides a comprehensive framework for developing an automatic Tok Pisin part-of-speech tagger. The resulting gold standard dataset, CoNLL-U formatted file, and trained UDPipemodel can be used for training, testing, and further development. Enhancements could include refining the tagging accuracy, exploring neural methods, and expanding the dataset for more extensive coverage.

A further project with this data implemented for an automatic NER recognition system for Tok Pisin has also been developed and will be appended soon. 
