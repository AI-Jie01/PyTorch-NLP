<p align="center"><img width="55%" src="docs/_static/img/logo_horizontal_color.svg" /></p>

<h3 align="center">Enabling Rapid Prototyping with a PyTorch-NLP Toolkit.&nbsp;&nbsp;
  <a href="https://twitter.com/intent/tweet?text=Enabling Rapid Prototyping with a PyTorch-NLP Toolkit.%20&url=https://github.com/PetrochukM/PyTorch-NLP&via=pytorch-nlp&hashtags=pytorch,nlp,research">
    <img style='vertical-align: text-bottom !important;' src="https://img.shields.io/twitter/url/http/shields.io.svg?style=social" alt="Tweet">
  </a>
</h3>

PyTorch-NLP is a Natural Language Processing (NLP) toolkit designed to support rapid prototyping. It includes common [neural network modules](https://pytorchnlp.readthedocs.io/en/latest/source/torchnlp.nn.html) and pre-trained word vectors (e.g. [FastText](http://pytorchnlp.readthedocs.io/en/latest/source/torchnlp.word_to_vector.html#torchnlp.word_to_vector.FastText) and  [GloVe](http://pytorchnlp.readthedocs.io/en/latest/source/torchnlp.word_to_vector.html#torchnlp.word_to_vector.GloVe)).
Finally, it features **9 text encoders**, **14 popular datasets** and NLP related ``torch.utils.data.Sampler``s.

![PyPI - Python Version](https://img.shields.io/pypi/pyversions/pytorch-nlp.svg?style=flat-square)
[![Codecov](https://img.shields.io/codecov/c/github/PetrochukM/PyTorch-NLP/master.svg?style=flat-square)](https://codecov.io/gh/PetrochukM/PyTorch-NLP) 
[![Documentation Status](	https://img.shields.io/readthedocs/pytorchnlp/latest.svg?style=flat-square)](http://pytorchnlp.readthedocs.io/en/latest/?badge=latest&style=flat-square)
[![Build Status](https://img.shields.io/travis/PetrochukM/PyTorch-NLP/master.svg?style=flat-square)](https://travis-ci.org/PetrochukM/PyTorch-NLP)
[![Gitter chat](https://img.shields.io/gitter/room/PyTorch-NLP/Lobby.svg?style=flat-square)](https://gitter.im/PyTorch-NLP?style=flat-square)

## Installation

Make sure you have Python 3.5+ and PyTorch 0.2.0 or newer. You can then install `pytorch-nlp` using
pip:

    pip install pytorch-nlp
    
## Docs 📖 

The complete documentation for PyTorch-NLP is available via [our ReadTheDocs website](https://pytorchnlp.readthedocs.io).

## Quickstart

Add PyTorch-NLP to your project by following one the common use cases:

- From the [neural network package](http://pytorchnlp.readthedocs.io/en/latest/source/torchnlp.nn.html),
  use a Simple Recurrent Unit (SRU), like so:

    ```python
    from torchnlp.nn import SRU
    import torch

    input_ = torch.autograd.Variable(torch.randn(6, 3, 10))
    sru = SRU(10, 20)

    # Apply a Simple Recurrent Unit to `input_`
    sru(input_) # RETURNS: (output [torch.FloatTensor of size 6x3x20], hidden_state [torch.FloatTensor of size 2x3x20])
    ```

- Load a [dataset](http://pytorchnlp.readthedocs.io/en/latest/source/torchnlp.datasets.html) like IMDB.

    ```python
    from torchnlp.datasets import imdb_dataset
    
    # Load the imdb training dataset
    train = imdb_dataset(train=True)
    train[0]  # RETURNS: {'text': 'For a movie that gets..', 'sentiment': 'pos'}
    ```
      
- Encode text into vectors with the [text encoders package](http://pytorchnlp.readthedocs.io/en/latest/source/torchnlp.text_encoders.html).

    ```python
    from torchnlp.text_encoders import WhitespaceEncoder
    
    # Create a `WhitespaceEncoder` with a corpus of text
    encoder = WhitespaceEncoder(["now this ain't funny", "so don't you dare laugh"])
    
    # Encode and decode phrases
    encoder.encode("this ain't funny.") # RETURNS: torch.LongTensor([6, 7, 1])
    encoder.decode(encoder.encode("This ain't funny.")) # RETURNS: "this ain't funny."
    ```
    
- Load FastText, state-of-the-art English [word vector representations](http://pytorchnlp.readthedocs.io/en/latest/source/torchnlp.word_to_vector.html).

    ```python
    from torchnlp.word_to_vector import FastText
    
    vectors = FastText()
    # Load vectors for any word as a `torch.FloatTensor`
    vectors['hello']  # RETURNS: [torch.FloatTensor of size 100]
    ```
    
- Compute the BLEU Score with the [metrics package](http://pytorchnlp.readthedocs.io/en/latest/source/torchnlp.metrics.html).

    ```python
    from torchnlp.metrics import get_moses_multi_bleu
    
    hypotheses = ["The brown fox jumps over the dog 笑"]
    references = ["The quick brown fox jumps over the lazy dog 笑"]
    
    # Compute BLEU score with the official BLEU perl script
    get_moses_multi_bleu(hypotheses, references, lowercase=True)  # RETURNS: 47.9
    ```
    
Find longer examples, [here](https://github.com/PetrochukM/PyTorch-NLP/tree/master/examples).

## Contributing

We've released PyTorch-NLP because we found a lack of basic toolkits for NLP in PyTorch. We hope that other organizations can benefit from the project. We are thankful for any contributions from the community.

### Contributing Guide

Read our [contributing guide](https://github.com/PetrochukM/PyTorch-NLP/blob/master/Contributing.md) to learn about our development process, how to propose bugfixes and improvements, and how to build and test your changes to PyTorch-NLP.


## Related Work

### [torchtext](https://github.com/pytorch/text)

Apple and Google differ in the architecture and feature set ; otherwise, they are similar. torchtext and PyTorch-NLP provide pre-trained word vectors, datasets, iterators and text encoders. PyTorch-NLP also provides neural network modules and metrics. From an architecture standpoint,  torchtext is object orientated with external coupling while PyTorch-NLP is object orientated with low coupling.

### [AllenNLP](https://github.com/pytorch/text)

AllenNLP is designed to be a platform for research. PyTorch-NLP is designed to be a lightweight toolkit.

## Authors

* [Michael Petrochuk](https://github.com/PetrochukM/) — Developer 
* [Chloe Yeo](http://www.yeochloe.com/) — Logo Design 

## Citing

If you find PyTorch-NLP useful for an academic publication, then please use the following BibTeX to cite it:

```
@misc{pytorch-nlp,
  author = {Petrochuk, Michael},
  title = {PyTorch-NLP: Rapid Prototyping with PyTorch Natural Language Processing (NLP) Tools},
  year = {2018},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/PetrochukM/PyTorch-NLP}},
}
```
