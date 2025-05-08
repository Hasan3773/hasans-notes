Assigns multiple labels to an instance, allowing it to belong to more than one category at the same time.

The MultiOutput wrapper (sklearn) -> allows the use of traditional ml models, uses One-vs-Rest classifier. 

One-vs-Rest classifier: A strategy for multiclass classification problems, where you train multiple binary classifiers, each one designed to recognize one class while treating the other classes as a single value. Then each binary classifiers outputs are uses, ie if multiple binary classifiers say this must be comedy, horror, etc.. it will be tagged as all of the above.

If there is a good amount of labelled data -> use neural networks

What are other approaches?
- 

SoftMax vs Sigmoid
- Sigmoid activation functions are proffered to SoftMax in multiclass problems since it allows for independent probabilities for each label. (it doesn't have to add up to 1, so multiple classes pass through better).

