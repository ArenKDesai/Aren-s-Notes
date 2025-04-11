
## Overview
From [Comprehensive Overview of Named Entity Recognition: Models, Domain-Specific Applications and Challenges](https://arxiv.org/abs/2309.14084) by Kalyani Pakhale (2023).

**Named Entity Recognition (NER)** is a text processing task that identifies named things and their types (2.1). To extend this notion, **Nested Named Entity Recognition** identifies the hierarchies these entities exist in. 
There are three main categories of NER:
1. **Rule-based Approaches**: Experts use domain knowledge to generate a vocabulary. 
2. **Supervised Learning Approaches**: Humans explicitly label instances of designated entity types and train machine learning (ML) models on them.  
3. **Unsupervised Approaches**: Provide a few "seed" instances, like a mini-vocabulary, and have an ML model learn rules from sentences containing these entity instances.
The modern approaches use neural networks (NNs) like convolutional neural networks (CNNs), long-short term memory networks (LSTMs), and transformers like **BERT**. 

### BERT as NER
Pre-trained BERT, the Bidirectional Encoder Representation from Transformers, can be fine-tuned with one more output layer for NER (3.1):
![[Screenshot 2025-04-11 152225.png]]
Grid-based document representations can allow BERT to encode the textual *and* layout information as a 2D feature map to improve model performance. This is commonly called a **BERTgrid** model, one of which being the **ViBERTgrid** model. 

## ViBERTgrid
From [ViBERTgrid: A Jointly Trained Multi-Modal 2D Document Representation for Key Information Extraction from Documents](https://arxiv.org/abs/2105.11672) by Lin et al. 
An example implementation of ViBERTgrid with PyTorch by ZeningLin on GitHub can be found [here](https://github.com/ZeningLin/ViBERTgrid-PyTorch#).

**Key Information Extraction (KIE)** is a pivotal task to extract values of pre-defined key fields from documents (1). Most models treat KIE as a token classification problem and solve it with deep learning models with either a **sequence-based**, **graph-based**, or **grid-based** approach. As mentioned above, BERTgrid is one of these models. 