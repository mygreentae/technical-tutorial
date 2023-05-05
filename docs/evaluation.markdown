---
layout: default
title: Evaluation and Testing
nav_order: 6
permalink: /Evaluation
---
# Evaluating a TTS model
One of the questions we need to ask when creating a TTS model is, how do we know that it is doing well? And, how do we improve? This secion will provide an overview on how to evaluate your model and how to improve it.

## How do you know your model is doing well?
There are basically two approaches that you may what to take: a subjective or an objective evaluation. The most popular subjective evaluation metric is the MOS (mean opinion score test). The most popular objective evaluation is the MCD tst (mel cepstral distortion). 

### Mean Opinion Score Test
One of the most popular metric for a subjective evaluation is the MOS test (mean opinion score test). This score is obtained by having a group of people rate the quality of the audio samples produced by the model. This might not be feasible for a small project because of the requirement of humans to rate these samples. MOS scores might also bare the weight of bias due to expectations of the people rating the samples. However for a project on a small scale like this, you can easily tell the quality of the synthesized speech with either the background noise, or if the speech is intelligible.

### Mel Ceptral Distortion
One of the most popular metric for an objective evaluation is the MCD test (mel ceptral distortion test). This test will compare two sequences of mel cepstra to  tell us the difference between them. There is a [MCD Python library](hhttps://pypi.org/project/pymcd/) where we can use our testing data to see how our model does compared to the audio sample recorded by a human.

#### How to calculate MCD
To evaluate our model using the MCD test, we first want to install the library:

```
$ pip install pymcd
```

Now, to find the MCD of an audio file, we can create a Python script to help us like so:

```python
from pymcd.mcd import Calculate_MCD

# instance of MCD class
# three different modes "plain", "dtw" and "dtw_sl" for the above three MCD metrics
mcd_toolbox = Calculate_MCD(MCD_mode="plain")

# two inputs w.r.t. reference (ground-truth) and synthesized speeches, respectively
mcd_value = mcd_toolbox.calculate_mcd("001.wav", "002.wav")
```

Then to run our MCD script:
```
python3 calculateMCD.py
```

#### MCD results 

{: .note}
The audio and texts are on [this](synthesis) page!

For the dataset we have been working with, here our results (for select audio files)! 

```
Text 1:
Text 2:
Text 3:
Text 4:
```

## Fine Tuning Your Model
If you are looking to improve your model, you might find some of these tips useful! 

### Changing parameters
One of the things we might want to change are the model's parameters. There might be a special combination of parameters that make your model produce a higher quality sound. For example, we can increase or decrease the number of iterations, or we can change the batch sizes. 

### Finding a new dataset
Another thing that we might want to change is to find a new dataset. One possibility is that the audio clips in the data set are too noisy, so the model is learning the noise, too. So, a dataset with audio with as minimal background noise as possible might help with improving your model.