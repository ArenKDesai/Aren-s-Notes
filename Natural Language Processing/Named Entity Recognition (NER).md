From [Comprehensive Overview of Named Entity Recognition: Models, Domain-Specific Applications and Challenges](https://arxiv.org/abs/2309.14084) by Kalyani Pakhale (2023).

## Overview
**Named Entity Recognition (NER)** is a text processing task that identifies named things and their types (2.1). To extend this notion, **Nested Named Entity Recognition** identifies the hierarchies these entities exist in. 
There are three main categories of NER:
1. **Rule-based Approaches**: Experts use domain knowledge to generate a vocabulary. 
2. **Supervised Learning Approaches**: Humans explicitly label instances of designated entity types and train machine learning (ML) models on them.  
3. **Unsupervised Approaches**: Provide a few "seed" instances, like a mini-vocabulary, and have an ML model learn rules from sentences containing these entity instances.
The modern approaches use neural networks (NNs) like convolutional neural networks (CNNs), long-short term memory networks (LSTMs), and transformers like **BERT**. 

### BERT as NER
Pre-trained BERT, the Bidirectional Encoder Representation from Transformers, can be fine-tuned with one more output layer for NER (3.1):
![[Screenshot 2025-04-11 152225.png]]
A few models have been created with this extra output layer and fine-tuned for performance in certain fields, such as the **Vi