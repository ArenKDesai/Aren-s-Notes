## Sequences
In order to model sequences, we need to be able to handle variable-length (non-fixed length) sequences. They also need to track long-term dependencies, where a variable at a smaller time step may influence an outcome near the end of the time steps. Order needs to be maintained, and parameters need to be shared across the sequence. 

### Predict the Next Word
This is an example for a sequencing problem. Imagine we have this sentence:
"This morning I took my cat for a \_\_\_\_."
The next word is *walk*, but the model doesn't know that. How do we get it to guess?

First, we need to represent words as numbers. This is so the neur