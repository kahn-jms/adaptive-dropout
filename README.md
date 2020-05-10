# Adaptive dropout

This is an example of dropout which varies according to the difference between vlidation and training accuracy.
Note that this is not the same as [Standout](https://papers.nips.cc/paper/5032-adaptive-dropout-for-training-deep-neural-networks.pdf), which is also known as adaptive dropout.

I do not claim to have invented this, I'm sure someone else has done this already.
This is just a mini programming exercise for myself to practice PyTorch.

## Concept

The underlying idea is simple: the dropout rate should increase with overfitting.
The simplest means of doing so is to set dropout = (1 - val_acc / train_acc).

A maximum and minimum level should also be set to handle the following cases:
* Validation accuracy is higher than training accuracy.
* Validation accuracy is so low that dropout approaches one, severely damaging network performance.

Therefore wrapping the basic dropout calculation in a `min()` and `max()` is advised.
