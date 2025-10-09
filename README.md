# OMAPL Corpus

## Overview

The OMAPL Corpus is a comprehensive Mandarin pronunciation assessment dataset comprising **82** Mandarin utterances from native speakers and **1,768** Mandarin utterances from French L1 speakers learning Mandarin. Each utterance has been meticulously annotated by four experts with professional Mandarin teaching experience at both the word and sentence levels.
#### Link: https://www.isca-archive.org/interspeech_2025/hsieh25b_interspeech.html


## Corpus Statistics

- **Total Audio Files**: 1,850 `.wav` files
- **Native Audio Files**: 82 `.wav` files
- **Non-native Audio Files**: 1768 `.wav` files
- **Total Speakers**: 49 speakers
- **Native Speakers**: 3 speakers (SPEAKER01*)
- **French Learners**: 46 speakers (SPEAKER02*)

Audio utterances from native speakers provide reference pronunciations for comparison with French learner productions.

The French learner demographics include 21 first-year students (5 males sand 16 females) and 25 second-year students (8 males and 17 females).

## Directory Structure

The corpus is organized as follows:

```
OMPAL/
├── README.md                     # This documentation file
├── native_scores.json    # Scores for native speakers
├── non-native_scores.json    # Scores for non-native speakers
├── non-native_scores-detail.json # Detailed scores for non-native speakers
├── train/                       # Training data splits
│   ├── train_1_scores.json     # Training set 1 annotations
│   ├── train_2_scores.json     # Training set 2 annotations
│   ├── train_3_scores.json     # Training set 3 annotations
│   ├── train_4_scores.json     # Training set 4 annotations
│   └── train_5_scores.json     # Training set 5 annotations
├── test/                        # Test data splits
│   ├── test_1_scores.json      # Test set 1 annotations
│   ├── test_2_scores.json      # Test set 2 annotations
│   ├── test_3_scores.json      # Test set 3 annotations
│   ├── test_4_scores.json      # Test set 4 annotations
│   └── test_5_scores.json      # Test set 5 annotations
└── wav/                         # Audio files organized by speaker
    ├── SPEAKER01001/            # Native Speaker 1 (20 files)
    │   ├── 00100101.wav
    │   ├── 00100102.wav
    │   └── ...
    ├── SPEAKER01002/            # Native Speaker 2 (29 files)
    │   ├── 00100201.wav
    │   └── ...
    ├── SPEAKER01003/            # Native Speaker 3 (33 files)
    │   ├── 00100301.wav
    │   └── ...
    ├── SPEAKER02001/            # French Learner 1
    ├── SPEAKER02002/            # French Learner 2
    ├── ...
    └── SPEAKER02046/            # French Learner 46
```




### File Naming Convention

#### Audio Files
- Format: `{speaker_id}{utterance_id}.wav`
- Example: `00100101.wav` (Speaker 01001, Utterance 01)
- Example: `00200201.wav` (Speaker 02002, Utterance 01)


## Annotation & Scoring Metrics

All utterances were independently annotated by **four seasoned experts who specialize in teaching Chinese as
a second language** and are paid by the hour. Annotations include per-word correctness (tone/segment) and sentence-level ratings on three dimensions: Accuracy, Fluency and Prosody.


### Word-level (Tone / Consonant / Vowel) ratings

| Score | Meaning |
|:-----:|---------|
| 1     | The pronunciation is correct. |
| 0     | The pronunciation is incorrect. |


### Sentence-level ratings

All sentence-level ratings are integers from 1 (worst) to 5 (best). They are provided on three dimensions:

#### Accuracy

| Score | Description |
|:-----:|-------------|
| 5     | The overall pronunciation and tone in the sentence are excellent, with no obvious mistakes. |
| 4     | The overall pronunciation and tone in the sentence are decent, with few mistakes. |
| 3     | Although there are some pronunciation and tone errors, they do not affect the overall understanding of the sentence. |
| 2     | Poor pronunciation as well as many pronunciation and tone errors. |
| 1     | Very poor pronunciation and only a few words in the sentence are understandable. |

#### Fluency

| Score | Description |
|:-----:|-------------|
| 5     | Very fluent. |
| 4     | Fluent in general, with only a few pauses in some places. |
| 3     | Moderately fluent, with multiple pauses but no break errors in a sentence. |
| 2     | Disfluent, with multiple pauses and break errors in a sentence. |
| 1     | Very disfluent. |

#### Prosody

| Score | Description |
|:-----:|-------------|
| 5     | Natural intonation at a stable speaking speed, speak with a cadence that sounds just like a native speaker. |
| 4     | Natural intonation at a mostly stable speaking speed but with little stammering and few unusual pauses. |
| 3     | Unstable speech speed, sometimes fast and sometimes slow with little stammering and few unusual pauses. |
| 2     | Unstable speech speed with lots of unusual pauses. |
| 1     | Unstable speech speed, unable to read a complete sentence. |

### JSON Format Example

The annotation data is structured in JSON format. Here's an example from `train/train_1_scores.json`:

```json
{
    "00200101": {                                 # Audio file id
        "accuracy": 4.33,                         # Sentence-level accuracy score
        "fluency": 4.67,                          # Sentence-level fluency score
        "prosody": 4,                             # Sentence-level fluency score
        "text": "他們都很忙",                       # Reference text
        "words": [
            {
                "phoneme_consonant": 1,           # Consonant correctness
                "phoneme_vowel": 1,               # Vowel correctness
                "tone": 1,                        # Tone correctness
                "text": [                         # Word text
                    "他"
                ]
            },
            {
                "phoneme_consonant": 1,
                "phoneme_vowel": 1,
                "tone": 1,
                "text": [
                    "們"
                ]
            },
            {
                "phoneme_consonant": 1,
                "phoneme_vowel": 1,
                "tone": 1,
                "text": [
                    "都"
                ]
            },
            {
                "phoneme_consonant": 1,
                "phoneme_vowel": 1,
                "tone": 1,
                "text": [
                    "很"
                ]
            },
            {
                "phoneme_consonant": 1,
                "phoneme_vowel": 0,
                "tone": 1,
                "text": [
                    "忙"
                ]
            }
        ]
    }
}
```

## Experimental Setup

To ensure a robust evaluation of the model’s performance on the OMPAL corpus for pronunciation assessment, five speaker combinations were randomly selected as test sets using a balancing criteria that balanced gender and proficiency levels. The remaining 42 non-native speakers were used for training. Given the relatively small size of the corpus, this setup enables a more reliable and stable validation of the model’s performance.

### Balancing Criteria
Each test combination ensures:
- **Native reference**: 4 non-native speakers and 1 native speaker
- **Gender balance**: Minimum 2 male and 2 female speakers
- **Proficiency balance**: At least 2 first-year and 2 second-year speakers
- **Score Classification**: 46 French learners categorized into 4 levels based on quartile divisions of average pronunciation scores

### Test Set Combination Details

Combination 1: ['01002', '02031', '02015', '02005', '02045'], 193 utterances 
- Speaker 01002: Male, Score 15.00, Native
- Speaker 02031: Female, Score 12.23, Second-year  
- Speaker 02015: Female, Score 11.05, First-year
- Speaker 02005: Male, Score 9.95, First-year
- Speaker 02045: Male, Score 9.76, Second-year

Combination 2: ['01003', '02006', '02021', '02038', '02041'], 197 utterances
- Speaker ID: 01003, Gender: Female, Score 15.00, Native
- Speaker ID: 02041, Gender: Male, Score: 12.00, Second-year
- Speaker ID: 02038, Gender: Female, Score: 11.19, Second-year
- Speaker ID: 02006, Gender: Female, Score: 10.40, First-year
- Speaker ID: 02021, Gender: Male, Score:  8.50, First-year


Combination 3: ['01003', '02021', '02022', '02031', '02036'], 197 utterances
- Speaker ID: 01003, Gender: Female, Score 15.00, Native
- Speaker ID: 02031, Gender: Female, Score: 12.23, Second-year
- Speaker ID: 02036, Gender: Female, Score: 11.16, Second-year
- Speaker ID: 02022, Gender: Male, Score: 10.40, First-year
- Speaker ID: 02021, Gender: Male, Score: 8.50, First-year


Combination 4: ['01002', '02001', '02007', '02029', '02030'], 160 utterances
- Speaker ID: 01002, Gender: Male, Score 15.00, Native
- Speaker ID: 02029, Gender: Male, Score: 11.39, Second-year
- Speaker ID: 02001, Gender: Female, Score: 10.85, First-year
- Speaker ID: 02007, Gender: Female, Score: 10.35, First-year
- Speaker ID: 02030, Gender: Male, Score: 9.86, Second-year


Combination 5: ['01001', '02005', '02021', '02041', '02043'], 183 utterances
- Speaker ID: 01001, Gender: Female, Score 15.00, Native
- Speaker ID: 02041, Gender: Male, Score: 12.00, Second-year
- Speaker ID: 02043, Gender: Female, Score: 11.07, Second-year
- Speaker ID: 02005, Gender: Male, Score: 9.95, First-year
- Speaker ID: 02021, Gender: Male, Score: 8.50, First-year


Given the relatively small corpus size, we implement 5-fold cross-validation where each test set serves as a validation fold. This approach maximizes data utilization while ensuring robust model evaluation across diverse speaker demographics and proficiency levels.


## Licensing

OMPAL is licensed under the
Creative Commons Attribution 4.0 International (CC BY 4.0) License.

You are free to share (copy and redistribute) and adapt (remix, transform, and build upon) the material for any purpose, even commercially, as long as you give appropriate credit.

**To view a copy of this license, visit:**
https://creativecommons.org/licenses/by/4.0/

## Citation
Please cite our paper if you find this work useful:

```bibtex
@inproceedings{hsieh25b_interspeech,
  title     = {{OMPAL: Bridging Speech and Learning with an Open-Source Mandarin Pronunciation Assessment Corpus for Global Learners}},
  author    = {Wen-Wei Hsieh and Hao-Wei Chi and Kuan-Chen Wang and Ping-Cheng Yeh and Te-hsin Liu and Chen-Yu Chiang},
  year      = {2025},
  booktitle = {{Interspeech 2025}},
  pages     = {2415--2419},
  doi       = {10.21437/Interspeech.2025-983},
  issn      = {2958-1796},
}
```