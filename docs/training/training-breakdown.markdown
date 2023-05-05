---
layout: default
title: Recipe Breakdown
nav_order: 1
permalink: /training-breakdown
parent: Training a Model
---
# How to Train Your Chinese TTS model using  VITS
This section will breakdown the recipe we will be using to train a Chinese TTS Model using VITS. If you would like to see the recipe in its full plese go to [this](training-full-recipe) page.

## Directory Structure
Our current directory structure for our whole project should look like this
```
Chinese-TTS-Model/
    | /dataset
    | /TTS
```
The `dataset` folder is the same folder as described in the [dataset prep](datasets/dataset-prep.markdown/#directory-structure) section. The `TTS` directory is the cloned CoquiTTS repository as descriped in the [installation guide](installation/#local-installation).

## Creating Your Training Recipe
As mentioned, we will be using customizing the CoquiTTS VITS recipe for a Chinese TTS model. The default recipe that CoquiTTS provides for us can be found here:
```
TTS/recipes/ljspeech/vits_tts/train_vits.py
```

We will be putting copying that file to the `TTS` folder and renaming it to `ChineseTTSModel.py`. The following sections will provide a full basic breakdown of the recipe and the modifications for a Chinese TTS model.

### Loading Your Dataset
First we will want to load our dataset. If you haven't formatted your data into the LJ Speech dataset format, please take a look at the [dataset prep](datasets/dataset-prep.markdown) section of the guide. 
```
dataset_config = BaseDatasetConfig(
    formatter="ljspeech", meta_file_train="metadata.txt", path=os.path.join(output_path, "../dataset/")
)
```
### Audio Configuration
We next want to load the audio. This will tell the model how it should be deschphering the audio.
```
audio_config = VitsAudioConfig(
    sample_rate=22050, win_length=1024, hop_length=256, num_mels=80, mel_fmin=0, mel_fmax=None
)
```
The configuration can be changed for some experimentation.

### Model Configuration
This part of the recipe defines the parameters our Chinese TTS model will train at. The configuration is slighly different from the default parameters in the recipe we were looking at because the language the provided recipe is for English. For Mandarin Chinese, CoquiTTS has many components that users can use for the ease of training TTS models. For example, there is a built in Mandarin Chinese phoneme set and text cleaner. 

{: .note }
You can still use CoquiTTS on languages that aren't built into the toolkit! It will be a but harder to get results tho.

The modified recipe to support Chinese is below:
```
config = VitsConfig(
    audio=audio_config,
    run_name="vits_ljspeech",
    batch_size=16,
    eval_batch_size=8,
    batch_group_size=5,
    num_loader_workers=8,
    num_eval_loader_workers=4,
    run_eval=True,
    test_delay_epochs=-1,
    epochs=250,
    text_cleaner="chinese_mandarin_cleaners", 
    use_phonemes=True,
    phoneme_language="zh-cn",
    phoneme_cache_path=os.path.join(output_path, "phoneme_cache"),
    compute_input_seq_cache=True,
    print_step=25,
    print_eval=True,
    mixed_precision=True,
    output_path=output_path,
    datasets=[dataset_config],
    cudnn_benchmark=False,
)
```
Parameters can be experimented with to fine-tune results.

### Initialization
We need to initialize the audio processor which is used for feature extraction and for the audio input and output. 
```
ap = AudioProcessor.init_from_config(config)
```

The tokenizer is used to convert the text to sequences of strings. If the model configuration doesn't specify the tokenizer, it will use the default.
```
tokenizer, config = TTSTokenizer.init_from_config(config)
```

This loads the data samples. Each sample is a list of `[text, audio_file_path, speaker_name]`. This can be constomized.
```
train_samples, eval_samples = load_tts_samples(
    dataset_config,
    eval_split=True,
    eval_split_max_size=config.eval_split_max_size,
    eval_split_size=config.eval_split_size,
)
```

Now, we initialize the model and the trainer!
```
model = Vits(config, ap, tokenizer, speaker_manager=None)

trainer = Trainer(
    TrainerArgs(),
    config,
    output_path,
    model=model,
    train_samples=train_samples,
    eval_samples=eval_samples,
)
trainer.fit()
```

## Training your Chinese TTS Model
To start training your model, you can run this command:

```
python3 ChineseTTSModel.py
```