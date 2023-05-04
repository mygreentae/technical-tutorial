---
layout: default
title: Finding a Dataset
nav_order: 3
permalink: /finding-a-dataset
parent: Datasets
---
# How to Find a Dataset
This section of the guide is about finding a dataset. There are many things to consider when finding the right dataset for our purposes. For example, do we want more data? This might mean we need to sacrifice the quality of our data. Do we want higher quality data? This might mean we need to have less data. These are some of the aspects we might need to consider. More information in the next section of this page!
## Quality versus Quantity
When picking out our dataset, we might want to consider what type of inputs we are going to have and what we want to output. For a text-to-speech model, we input text and we output speech. This means we want our model to pick up text well, and produce as natural sounding as possible speech. So our dataset for a TTS model, should be made of as many words as possible so the model can learn how to make as many sounds as possible, and with high quality audio so our model produces the most natural sounding voice possible.

Now we can ask these questions:
1. Do we want to have multiple speakers? Is more than one speaker needed for a model to have the most natural sounding speech?
1. Do we want a single speaker? Is one speaker enough for the TTS model to have the most natural sounding speech?
1. Does a TTS model learn better though female speakers? Does a TTS model learn better though male speakers?
1. Do we want to have various types of text? Do we need to have a variety of types of text to be able to learn as many sounds as possible?
1. Do we want to have a single type of text? Is a single text enough to learn an adequate amount of words?

These questions can help us find the best dataset for your purposes and what you want to test or play around with.
## Dataset Examples
1. [CSS10: A Collection of Single Speaker Speech Datasets for 10 Languages](https://github.com/Kyubyong/css10) - This is a collection of datasets from 10 different languages, which includes Mandarin Chinese. The Chinese dataset is comprised of a single female Chinese speaker reading two different stories  朝花夕拾 (Chao Hua Si She) and 呐喊 (Call to Arms). This dataset is relatvely small with just ovr 6 hours.
1. [AISHELL-3](http://www.openslr.org/93/) - This is an open source large scale high-fidelity multi-speaker Mandarin dataset. This dataset has about 85 hours of audio by 218 native Chinese Speakers. The documentation also includes other attributes to each speaker (such as gender, age, native accents) which can be useful if you want to test which attributes work best for your model.
1. [WenetSpeech](https://paperswithcode.com/dataset/wenetspeech) - This is a multi-domain Mandarin dataset consisting of over 10,000 ours of high-quality labeled speech, over 2,400 hours of weakly labeled speech, and over 10,000 hours of unlabeled speech. 

## Dataset I used
For the synthesized audio you will hear through out the guide, the dataset I used was from the CSS10 dataset.