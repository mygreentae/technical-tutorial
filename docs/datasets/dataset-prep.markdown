---
layout: default
title: Dataset Praparation
nav_order: 2
permalink: /dataset-prep
parent: Datasets
---
# How to Prepare Your Data
This section will be going over how to prepare your dataset for training. To train a TTS model, the speech must be divided into audio clips and each audio clip needs to have its now transcription.

## LJ Speech format
For our project, we will be using the [LJ Speech dataset](https://keithito.com/LJ-Speech-Dataset/) format. CoquiTTS already has a tool for the LJ Speech Dataset, so it will be easiest to structure our data in this way. 

### Directory Structure
Because we want to be able to separate our audio files from the transcription, we want to have a directory structure like shown below:
```
/dataset
    | /wavs
        | audio1.wav
        | audio2.wav
        ...
    | metadata.txt
```

In the case of the CSS10 dataset, our directory structure will look something like this:
```
/dataset
    | /call_to_arms
        | audio1.wav
        | audio2.wav
        ...
    | /chao_hua_si_she
        | audio1.wav
        | audio2.wav
    | metadata.txt
```

All of our audio files will be in a `.wav` format and put under the folder called `wavs`. This folder can be called anything. We will also have a text file called `metadata.txt` to keep all of our audio to transcription information.

### Audio Files
As mentioned above, our audio files should be in the `.wav ` format. If they aren't in that format, we will want to convert them into the `.wav` format. We can use this bash command to help us automate the process.

```
sox <filename>.<file-format> <filename>.wav
```
A sample bash script to convert all `.mp3` files in a certain folder to `.wav` files is shown below. You can edit this as you see fit to help with the conversion process
```bash
#!/bin/bash
for i in *.mp3
do
    sox "$i" "waves/$(basename "$i" .mp3).wav"
done
```

### Metadata Format
The `metadata.txt` file format should look like this:
```
<filename>|<transcription>
```
The delimiter between the two pieces of infromation is a `|`.

So, in the case of the CSS10 dataset, the metadata file originally looked something like this:
```
call_to_arms/call_to_arms_0000.wav|《呐喊》自序·鲁迅·我在年青时候也曾经做过许多梦，|nà hǎn zì xù · lǔ xùn · wǒ zài nián qīng shí hou yě céng jīng zuò guò xǔ duō mèng ，|8.9
call_to_arms/call_to_arms_0001.wav|后来大半忘却了，但自己也并不以为可惜。所谓回忆者，虽说可以使人欢欣，有时也不免使人寂寞，|hòu lái dà bàn wàng què liào ， dàn zì jǐ yě bìng bù yǐ wéi kě xī 。 suǒ wèi huí yì zhě ， suī shuō kě yǐ shǐ rén huān xīn ， yǒu shí yě bù miǎn shǐ rén jì mò ，|9.88
call_to_arms/call_to_arms_0002.wav|使精神的丝缕还牵着己逝的寂寞的时光，又有什么意味呢，而我偏苦于不能全忘却，|shǐ jīng shen dì sī lǚ huán qiān zháo jǐ shì dì jì mò dì shí guāng ， yòu yǒu shén me yì wèi ní ， ér wǒ piān kǔ yú bù néng quán wàng què ，|7.78
call_to_arms/call_to_arms_0003.wav|这不能全忘的一部分，到现在便成了《呐喊》的来由。我有四年多，曾经常常，|zhè bù néng quán wàng dì yī bù fen ， dào xiàn zài biàn chéng liào nà hǎn dì lái yóu 。 wǒ yǒu sì nián duō ， céng jīng cháng cháng ，|8.65
call_to_arms/call_to_arms_0004.wav|——几乎是每天，出入于质铺和药店里，|— — jī hū shì měi tiān ， chū rù yú zhí pù hé yào diàn lǐ ，|3.81
call_to_arms/call_to_arms_0005.wav|年纪可是忘却了，总之是药店的柜台正和我一样高，质铺的是比我高一倍，|nián jì kě shì wàng què liào ， zǒng zhī shì yào diàn dì guì tái zhèng hé wǒ yī yàng gāo ， zhì pù dì shì bì wǒ gāo yī bèi ，|8.01
call_to_arms/call_to_arms_0006.wav|我从一倍高的柜台外送上衣服或首饰去，在侮蔑里接了钱，再到一样高的柜台上给我久病的父亲去买药。|wǒ zòng yī bèi gāo dì guì tái wài sòng shàng yī fu huò shǒu shì qù ， zài wǔ miè lǐ jiē liào qián ， zài dào yī yàng gāo dì guì tái shàng jǐ wǒ jiǔ bìng dì fù qīn qù mǎi yào 。|10.46
call_to_arms/call_to_arms_0007.wav|回家之后，又须忙别的事了，因为开方的医生是最有名的，以此所用的药引也奇特：|huí jiā zhī hòu ， yòu xū máng bié de shì liào ， yīn wèi kāi fāng dì yī shēng shì zuì yǒu míng dì ， yǐ cǐ suǒ yòng dì yào yǐn yě qí tè ：|7.6
call_to_arms/call_to_arms_0008.wav|冬天的芦根，经霜三年的甘蔗，蟋蟀要原对的，结子的平地木，多不是容易办到的东西。|dōng tiān dì lú gēn ， jīng shuāng sān nián dì gān zhe ， xī shuài yào yuán duì dì ， jié zi dì píng dì mù ， duō bù shì róng yì bàn dào dì dōng xi 。|8.52
call_to_arms/call_to_arms_0009.wav|然而我的父亲终于日重一日的亡故了。有谁从小康人家而坠入困顿的么，|rán ér wǒ dì fù qīn zhōng yú rì zhòng yī rì dì wáng gù liào 。 yǒu shéi zòng xiǎo kāng rén jiā ér zhuì rù kùn dùn dì me ，|8.32
call_to_arms/call_to_arms_0010.wav|逃异地，去寻求别样的人们。我的母亲没有法，办了八元的川资，说是由我的自便；然而伊哭了，|táo yì dì ， qù xún qiú bié yáng dì rén men 。 wǒ dì mǔ qīn méi yǒu fǎ ， bàn liào bā yuán dì chuān zī ， shuō shì yóu wǒ dì zì biàn ； rán ér yī kū liào ，|9.99
...
```
After formatting the data into the LJ Speech format, we got something that looks like this:
```
call_to_arms/call_to_arms_0000.wav|《呐喊》自序·鲁迅·我在年青时候也曾经做过许多梦，
call_to_arms/call_to_arms_0001.wav|后来大半忘却了，但自己也并不以为可惜。所谓回忆者，虽说可以使人欢欣，有时也不免使人寂寞，
call_to_arms/call_to_arms_0002.wav|使精神的丝缕还牵着己逝的寂寞的时光，又有什么意味呢，而我偏苦于不能全忘却，|shǐ jīng shen dì sī lǚ huán qiān zháo jǐ shì dì jì mò dì shí guāng ， yòu yǒu shén me yì wèi ní ， ér wǒ piān kǔ yú bù néng quán wàng què ，|7.78
call_to_arms/call_to_arms_0003.wav|这不能全忘的一部分，到现在便成了《呐喊》的来由。我有四年多，曾经常常，
call_to_arms/call_to_arms_0004.wav|——几乎是每天，出入于质铺和药店里，
call_to_arms/call_to_arms_0005.wav|年纪可是忘却了，总之是药店的柜台正和我一样高，质铺的是比我高一倍，
call_to_arms/call_to_arms_0006.wav|我从一倍高的柜台外送上衣服或首饰去，在侮蔑里接了钱，再到一样高的柜台上给我久病的父亲去买药。
call_to_arms/call_to_arms_0007.wav|回家之后，又须忙别的事了，因为开方的医生是最有名的，以此所用的药引也奇特：
call_to_arms/call_to_arms_0008.wav|冬天的芦根，经霜三年的甘蔗，蟋蟀要原对的，结子的平地木，多不是容易办到的东西。
call_to_arms/call_to_arms_0009.wav|然而我的父亲终于日重一日的亡故了。有谁从小康人家而坠入困顿的么，
call_to_arms/call_to_arms_0010.wav|逃异地，去寻求别样的人们。我的母亲没有法，办了八元的川资，说是由我的自便；然而伊哭了，
...
```
