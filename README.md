# TrellisNet for Sequence Modeling



This repository contains the experiments done in paper [Trellis Networks for Sequence Modeling](https://arxiv.org/abs/XXXX.XXXXX) by Shaojie Bai, J. Zico Kolter and Vladlen Koltun.



On the one hand, a trellis network is a temporal convolutional network with special structure, characterized by weight tying across depth and direct injection of the input into deep layers. On the other hand, we show that truncated recurrent networks are equivalent to trellis networks with special sparsity structure in their weight matrices. Thus trellis networks with general weight matrices generalize truncated recurrent networks. This allows trellis networks to serve as bridge between recurrent and convolutional architectures, benefitting from algorithmic and architectural techniques developed in either context. We leverage these relationships to design high-performing trellis networks that absorb ideas from both architectural families. Experiments demonstrate that trellis networks outperform the current state of the art on a variety of challenging benchmarks, including word-level language modeling on Penn Treebank and WikiText-103, character-level language modeling on Penn Treebank, and stress tests designed to evaluate long-term memory retention.


Our experiments were done in PyTorch. If you find our work, or this repository helpful, please consider citing our work:

```
@article{BaiTrellis2018,
	author    = {Shaojie Bai and J. Zico Kolter and Vladlen Koltun},
	title     = {Trellis Networks for Sequence Modeling},
	journal   = {arXiv:XXXX.XXXXX},
	year      = {2018},
}
```


## Datasets

The code should be directly runnable with PyTorch 0.4.0 (although slight modifications may be needed for other versions). This repository contains the training script for the following tasks:

- **Sequential MNIST** handwritten digit classification
- **Permuted Sequential MNIST** that randomly permutes the pixel order in sequential MNIST
- **Sequential CIFAR-10** classification (more challenging, due to more intra-class variations, channel complexities and larger images)
- **Penn Treebank (PTB)** word-level language modeling (with and without the mixture of softmax); vocabulary size 10K
- **Wikitext-103 (WT103)** large-scale word-level language modeling; vocabulary size 268K
- **Penn Treebank** medium-scale character-level language modeling

Note that these tasks are on very different scales, with unique properties that challenge sequence models in different ways. For example, word-level PTB is a small dataset that a typical model easily overfits, so judicious regularization is essential. WT103 is a hundred times larger, with less danger of overfitting, but with a vocabulary size of 268K that makes training more challenging (due to large embedding size).



## Usage

All tasks share the same underlying TrellisNet model, which is in file `trellisnet.py` (and the eventual models, including components like embedding layer, are in `model.py`). As discussed in the paper, TrellisNet is able to benefit significantly from techniques developed originally for RNNs as well as temporal convolutional networks (TCNs). Some of these techniques are also included in this repository. Each task is organized in the following structure:

```
[TASK_NAME] /
    data/
    [TASK_NAME].py
    model.py
    utils.py
```

where `[TASK_NAME].py` is the training script for the task (with argument flags; use `-h` to see the details).
