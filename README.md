LSTM encoder-decoder seq2seq model
==================================

This project is an implementation of a simple encoder-decoder seq2seq model in MxNet. The OpenNMT model is based on:

- a stacked LSTM encoder
- a stacked LSTM decoder
 
The reference model configuration is:

- 2 LSTM encoder layers
- 2 LSTM decoder layers
- hidden state of 500 units
- embedding size of 500 units
- truncating the vocabulary to the top 50,000 words
- truncating the maximum sentence length to 50 words

The reference model is normally trained on the WMT15 English-German dataset, which consists of:

- raw Europarl v7
- Common Crawl
- News Commentary v7

For more details, see [here](http://opennmt.net/Models/).
 
----------

How to run the scripts?
-------------------------------

 1. Run the `get_opennmt_data.sh` script to download and preprocess the dataset. Preprocessing includes corpora concatenation, shuffling, and a trainining/validation set split.
 2. Run the preprocessing step. Fair warning: this can take close to half an hour, but it's a one-time cost. Run `python preprocess_data.py` to do that. Make sure you have enough RAM, at least 32 GB.
 3. Run the model. Note that the batch size setting is global, not per GPU. So, when running on a DGX-1 with a batch size of 128 per GPU, choose a batch size of 128 * 8 = 1,024. Here is a sample command to run the training:

```python seq2seq_bucketing.py --num-layers 2 --num-embed 500 --num-hidden 500 --optimizer adam --disp-batches 1 --gpus 0,1 --num-epochs 1 --batch-size 256```

Credits
-------

Many thanks to Eric Xie (@piiswrong), Sheng Zha (@szha) and Antti-Pekka Hynninen (@ap-hynninen) for valuable input.

License
-------

This project is licensed under the Apache 2.0 license. See the text of the license [here](https://github.com/mkolod/mxnet_seq2seq/blob/master/LICENSE.txt).

> **Note:**

> Inference isn't implemented yet.

