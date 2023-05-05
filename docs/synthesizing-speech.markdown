---
layout: default
title: Synthesizing Speech
nav_order: 5
permalink: /synthesis
---
# Synthesizing Speech
Once our model finishes training, we can get on to synthesizing the speech and hearing what our model sounds like!

## How Do We Synthesize Speech?
CoquiTTS makes it really easy to synthesize speech. Here is how we can do that.

Make sure you are still in the `TTS` directory. Run this command:
```
$ tts --text "<text-to-be-synthesized>" \
    --model_path <path-to-model>/best_model.pth \
    --config_path <path-to-config>/config.json \
    --out_path output.wav
```
*note*: All of the paths should be in the TTS directory.

## Sample Synthesis
Here are some sample speech synthesized by the model we created. The human speech is also there so we can compare what the human created and what the model created. These are also all from the CSS10 dataset.

Text 1: 研究这一类三魂渺渺，七魄茫茫，“死无对证”的学问，是很新颖，也极占便宜的。

Human Produced:
<audio controls>
  <source src="audio/1137_real.wav" type="audio/wav">
</audio>

Synthesized:

Text 2: 这一点后记也或作或辍地几乎做了两个月。天热如此，汗流浃背，是亦不可以已乎：
Human Produced:
<audio controls>
  <source src="audio/1154_real.wav" type="audio/wav">
</audio>

Synthesized:

Text 3: 于是说，这忘八蛋要提防，或者不如吩咐地保，不许他住在未庄。

Human Produced:
<audio controls>
  <source src="audio/1169_real.wav" type="audio/wav">
</audio>

Synthesized:

Text 4: 他生平所知道的革命党只有两个，城里的一个早已“嚓”的杀掉了，现在只剩了一个假洋鬼子。

Human Produced:
<audio controls>
  <source src="audio/1240_real.wav" type="audio/wav">
</audio>

Synthesized:

