# [ShEMO-Modification]()
[![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.png?v=103)](https://github.com/ellerbrock/open-source-badges/)

This repository contains a modification on the Shemo dataset with help of an Automatic Speech Recognition (ASR) system.

For more information, please read our [paper]().

## Data Samples
The file ***modified_shemo.json*** contains the modified dataset samples with the following attributes.
```
"Name of the audio file": {
    "path": Path to the .wav file,
    "gender": The gender of the speaker,
    "speech_name": Name of the .wav file in the original dataset,
    "text_name": Name of the .ort file in the original dataset,
    "emotion": Emotional label based on text files,
    "transcript": Ground-Truth text transcription of the utterance,
    "ipa": Phonetic transcription of the utterance according to the IPA standard
}
```
Here is a sample of modified dataset:
```json
"F01A01.wav": {
    "path": "shemo/F01A01.wav",
    "gender": "female",
    "speech_name": "F01A01",
    "text_name": "F01A01",
    "emotion": "anger",
    "transcript": "\u062f\u06cc\u06af\u0647 \u0646\u0645\u06cc\u200e\u062a\u0648\u0646\u0645 \u062a\u062d\u0645\u0644 \u06a9\u0646\u0645.",
    "ipa": "dige nemitun\u04d5m t\u04d5h\u04d5mmol kon\u04d5m"
}
```

## Sharif Emotional Speech Database (ShEMO)
the ShEMO dataset contains 3000 audio files along with 3000 text files for each sentence as a ground-truth transcription. The text file of the sentence related to the corresponding audio file can be found through the names of the files. In fact, the audio and the text file of an utterance have the same name. But out of 3000 files, only 2838 have the same name. With further investigations, we found that some of these text files have the wrong names and referred to the wrong audio file. In the picture below, examples of errors in referencing audio and text files can be seen. We fixed the errors and inconsistencies in ShEMO dataset by using an Automatic Speech Recognition (ASR) system

<img src="https://user-images.githubusercontent.com/55990659/200169946-fb1d0af5-186a-4742-b5a1-f282aa861e44.PNG" alt="ShEMO errors" width="400"/>

## Contradictions Correction
To recognize the correct names of these files, a 4-gram language model on Web2Corpus was used. Thus, the ASR system, with the help of the language model, will recognize sentences more accurately. Then the sentences whose WER and CER metrics are more than 0.5 are compared with each other to find the correct text file. There are 347 files out of a total of 3000 files in the dataset that meet the mentioned conditions. The result of modifying the dataset is much fewer errors in sentence recognition. As shown in the table below, the WER in this dataset has been greatly reduced after correcting the text files related to each audio file.
| ShEMO Modification | Word Error Rate |
| --- | --- |
| Before | 51.97 |
| After | 30.79 |

## Labels Correction
After modifying the dataset, it was found that there are 163 files whose audio file labels are different from their text file labels. the table below, shows the result of testing a convolutional neural network model on the new dataset. In this experiment, these 163 files have been used as the test set and the rest of the files have been used to train the model. The better performance of the model by choosing the text file label as the final label of these 163 files shows that the text file label is the correct label for these files.
| Select Labels | Weighted Accuracy | Unweighted Accuracy |
| --- | --- | --- |
| .wav files | 33.55 | 22.55 |
| .ort files | 72.25 | 43.92 |

## Citation
Link to the original [ShEMO](https://github.com/pariajm/sharif-emotional-speech-dataset) dataset.

### contact
ali.yazdani@mail.sbu.ac.ir
