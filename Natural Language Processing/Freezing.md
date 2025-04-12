
## Overview
From the 2019 paper [What Would Elsa Do? Freezing Layers During Transformer Fine-Tuning](https://arxiv.org/abs/1911.03090) by Lee et al. 

Large pretrained models like BERT can take a long time and a lot of compute power to fine-tune, but research proves that only a few of the final layers actually need to be retrained to fine-tune a model effectively (1). Therefore, it can be more efficient to freeze layers of a transformer rather than always retraining the entire model. 
Prior research also shows that the earlier layers of a network extract universal features, while later layers perform task-specific modelling (2.2). This means that if a developer is fine-tuning a model for a specific task, they may want to freeze the early layers. 

Through case studies, the researchers propose that, when fine-tn
