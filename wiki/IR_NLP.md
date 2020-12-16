---
title: Information Retrieval and Natural Language Processing
layout: wiki
---

## Course Description

Information Retrieval (IR) is an area that aims at answering user information needs with the most relevant information. In this course we shall study how search applications, e.g. Google, compute relevant search results from a repository of Web information.

This course starts by dissecting a search engine, and discusses the fundamental techniques currently used in information retrieval. Afterwards, the most relevant algorithms and retrieval models are discussed in detail.

The current demand for intuitive search processes and language comprehension have been alligning Natural Language Processing (NLP) and IR. In this course you will learn fundamental techniques, that are used to encode syntax, grammar, and semantics in machines. 

This course includes extensive hands-on laboratories where key retrieval and NLP algorithms are examined. The goal is to strengthen students’ experimental analysis and critical thinking skills concerning search performance metrics and experimental results.

## Objectives
- Learn the concept of information relevance.
- Learn how to parse and analyze text data.
- Learn how to rank information by relevance.
- Analysis of experimental results.

## Grading
Exam (40%) + Lab work (60% with three submissions)

## Online Lectures and Discussion forum

All lectures and labs are thaught by Zoom. Please, contact instructors to access the meeting ID and password.

A discussion forum (Discord) is set up to let students and lecturers discuss course and project issues. Please ask the intructors to join.

### Discussion Forum Rules
When registering for the discussion forum, please follow the username schema: "FirstName Surname-StudentNr" e.g.: "Gustavo Gonçalves-40000"

## Schedule
- 23/set/20	[Introduction](/assets/files/a01 Introduction.pdf) ([video](https://youtu.be/Eak1ymcSIXs))
- 23/set/20	[Text processing, NGRAMS, cosine distance](/assets/files/a02 Basic techniques.pdf) ([video](https://youtu.be/Eak1ymcSIXs))
- 30/set/20	[Language models](/assets/files/a03 Language Models.pdf) ([video](https://youtu.be/hyijYuoZ0pA))
- 07/out/20	[Evaluation](/assets/files/a04 Evaluation.pdf) ([video](https://youtu.be/fkjqwZUPMGw))
- 14/out/20	[Relevance-based Language Models](/assets/files/a05 Relevance LM.pdf) ([video](https://youtu.be/XfLpRDD7aHE))
- 21/out/20	[Document categorization](/assets/files/a06 Document categorization.pdf) ([video](https://youtu.be/fO1X1wdw6FQ))
- 28/out/20	[Learning to rank](/assets/files/a07 Learning to rank.pdf) ([video](https://youtu.be/w48z48CrZYc))
- 04/nov/20	[Word embeddings](/assets/files/a08 Word embeddings.pdf) ([video](https://youtu.be/-D_6RjWzc_c))
- 11/nov/20	[Information extraction](/assets/files/a09 Information Extraction 2020.pdf) ([video](https://youtu.be/qzl4XYPjmck))
- 18/nov/20	[Question answering](/assets/files/a10 Question Answering.pdf) ([video](https://youtu.be/w58k1bJC2e0))
- 25/nov/20	[Conversational search](/assets/files/a11 Conversational search.pdf) ([video](https://youtu.be/2Rbg-6gS7fs))
- 02/dez/20	[Computational Ethics for NLP and IR](/assets/files/a12 Computational Ethics.pdf) ([video](https://))
- 09/dez/20 Project support
- 16/dez/20 Project support

## Labs
 - Project starting point [Colab Notebook](/assets/files/Project-Colab.zip) or [Jupyter Notebook](/assets/files/Project-Jupyter.zip)
 - Sentiment classification [with Scikit Learn](/assets/files/Sentiment_classification_scikit_learn.ipynb) \[[Colab Link](https://colab.research.google.com/drive/1zV24gqXke5eJXNkbWNLpfQCxUfcemx-T?usp=sharing)\] or [with PyTorch](/assets/files/SentimentClassification-Colab.ipynb) \[[Colab Link](https://colab.research.google.com/drive/1UQ43GXaI_4bsu79wY4CQ5af3kNQ2Lqa3?usp=sharing)\]
 - Word and Sentence embeddings [Part 1](https://colab.research.google.com/drive/1CAjsUFwK--3366jotyOr6Jxe__bMmyhi?usp=sharing) or [Part 2](https://colab.research.google.com/drive/19dXRLvO_FrtOLyvaX1JAaPmOX8XGPCgy?usp=sharin)
 - Named Entities \[[Colab Link](https://colab.research.google.com/drive/1SxajcE0YPz-qq6HGUiDlkYs2P2MPaTEx#scrollTo=PTDAyspiTL1-)\]
 - Query Re-Writing with T5 \[[Colab Link](https://colab.research.google.com/drive/14cV06j431JebnxqpZBPy2He7n7_55YIF#scrollTo=YxMDXF-Wl1__)\]

### Project guidelines for milestone 2:
 - Model training:
     - Build triplets (topic_turn, passage, relevance judgment) - Use only annotated ones;
     - Convert relevance labels to 0-1;
     - Feed all the pairs (topic_turn, passage) to BERT and get its embeddings;
     - Train classifier with the embeddings and use the relevance judgments as labels to separate relevant from non-relevant pairs (use the provided classifier);

 - Answer Retrieval w/ LMD + Re-ranking with Trained Classifier:
     - Get top-1000 passage from Elasticsearch;
     - Feed BERT with <topic_turn, passage> and extract CLS embedding for each passage;
     - Feed 1000 CLS embeddings to Classifier and extract scores;
     - Sort passges by scores.

## Exercises
[Exercises Sheet](/assets/files/Exercises.pdf)

## Lecturers
Joao Magalhaes (jmag@xfct.unlx.pt - remove the 'x's to mail us)

Gustavo Gonçalves (ggoncalv<img src="/assets/images/at_sign.png" alt=" " style="display:inline;margin:0;border-radius:0"/>cs.cmu.edu)
