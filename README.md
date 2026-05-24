# Final Project: Multiclass IMDb Sentiment Analysis

This repository contains an academic final project for the Python for Data Science course. The project explores multiclass sentiment analysis on movie reviews using modern Natural Language Processing (NLP) methods.

The goal is to classify movie reviews into three sentiment classes:

```text
0 = Negative
1 = Neutral
2 = Positive
```

This is a student project developed for learning, experimentation, and model comparison. The implementation focuses on building a complete NLP pipeline rather than a fully optimized production system.

## Overview

The original IMDb movie review dataset is commonly used for binary sentiment classification with two labels: positive and negative. In this project, the task is extended to multiclass sentiment analysis by adding a neutral class.

The project contains the following main stages:

1. Data preparation
2. Exploratory Data Analysis (EDA)
3. NLP preprocessing and text vectorization
4. Model training
5. Model evaluation
6. Lightweight web app demonstration

## Dataset

The final dataset is built from two main sources:

### IMDb Movie Reviews

The IMDb dataset provides positive and negative movie reviews.

- Negative reviews: label `0`
- Positive reviews: label `2`
- Total original IMDb samples: 50,000

### Neutral Reviews

A separate neutral review dataset is used to create the third class.

- Neutral reviews: label `1`
- Originally collected in Russian
- Translated into English
- Approximately 25,000 samples

After preprocessing and filtering, the final dataset contains around 72,000 samples.

## Data Preparation

The data preparation process includes:

- Loading IMDb positive/negative reviews
- Loading neutral reviews
- Standardizing labels
- Removing HTML tags
- Removing URLs
- Removing special characters and noisy tokens
- Lowercasing text
- Normalizing whitespace
- Merging datasets
- Filtering empty or very short reviews
- Splitting data into train, validation, and test sets

The split ratio is:

| Dataset | Ratio |
|---|---:|
| Training | 70% |
| Validation | 15% |
| Test | 15% |

## Exploratory Data Analysis

The EDA stage includes:

- Class distribution analysis
- Review length distribution
- Duplicate checking
- WordCloud visualization for each sentiment class

The dataset is near-balanced across the three classes, although the neutral class is slightly smaller after filtering.

## NLP Preprocessing

The project demonstrates common NLP preprocessing steps:

- Tokenization
- Stopword removal
- Lemmatization
- Text normalization
- TF-IDF vectorization
- Sequence tokenization for neural models

Different models require different text representations:

| Model | Text Representation |
|---|---|
| spaCy TextCategorizer | spaCy internal text representation |
| Logistic Regression | TF-IDF |
| Linear Regression baseline | TF-IDF |
| BiLSTM | Token sequences with embedding layer |

## Models

### 1. spaCy TextCategorizer

The main model is spaCy TextCategorizer with a CNN-based architecture.

The model follows the general pipeline:

```text
Text → Tokenization → tok2vec/CNN representation → Pooling → Softmax classification
```

The model is trained as a single-label multiclass classifier with three labels:

```text
neg
neu
pos
```

### 2. Logistic Regression with TF-IDF

Logistic Regression is used as a strong traditional machine learning benchmark.

The text is represented using TF-IDF with unigram and bigram features.

### 3. Linear Regression Baseline

Linear Regression is included as a simple baseline, although it is not designed for classification tasks.

The continuous prediction output is rounded and clipped into valid class labels.

### 4. BiLSTM

The BiLSTM model is used as a deep learning benchmark. It processes review text as token sequences and captures contextual information from both directions.

The architecture includes:

- Embedding layer
- Bidirectional LSTM layer
- Dropout
- Dense softmax output layer

## Results

### Model Comparison

| Model | Accuracy | F1 Macro | F1 Weighted |
|---|---:|---:|---:|
| spaCy TextCategorizer | 0.9121 | 0.9150 | 0.9120 |
| Logistic Regression | 0.9241 | 0.9246 | 0.9243 |
| Linear Regression | 0.6262 | 0.6330 | 0.6371 |
| BiLSTM | 0.8907 | 0.8945 | 0.8907 |

### Main Observations

Logistic Regression achieves the highest accuracy, but it depends heavily on the TF-IDF pipeline and manual preprocessing.

spaCy TextCategorizer provides a strong trade-off between accuracy, simplicity, and deployment convenience. It is lightweight and easier to integrate into an inference pipeline.

BiLSTM performs reasonably well but requires more computational resources and is less convenient for lightweight deployment.

Linear Regression performs poorly compared with classification models, as expected.

## Web App Demonstration

A lightweight demo app is implemented using Gradio.

The app allows users to:

- Enter a movie review
- Remove HTML tags from the input
- Predict sentiment using the trained spaCy model
- Display the predicted label and class probabilities

Example output format:

```text
pos (neg:0.0012 | neu:0.1091 | pos:0.8898)
```

## Limitations

This project is mainly an academic final project and an exploratory NLP implementation. Some limitations remain:

- The neutral dataset was translated from Russian to English, which may introduce translation artifacts.
- Some neutral samples may be noisy or weakly labeled.
- The CNN-based spaCy model mainly captures local n-gram features.
- Sarcasm, irony, and double negation remain difficult for the model.
- Hyperparameter tuning was not exhaustive.
- Transformer-based models such as BERT or DistilBERT were discussed as future improvements but were not the main deployment model.

## Future Work

Potential improvements include:

- Cleaning and refining the neutral dataset
- Removing or relabeling neutral outliers
- Applying back-translation and paraphrasing for data augmentation
- Fine-tuning transformer models such as BERT, DistilBERT, RoBERTa, or DeBERTa
- Improving the web app UI
- Deploying the model as a full API service
- Extending the system to multilingual sentiment analysis

## Repository Structure

```text
final-project-multiclass-imdb-sentiment-analysis/
├── app/
├── assets/
├── data/
│   └── README.md
├── notebooks/
│   └── multiclass_imdb_sentiment_analysis.ipynb
├── reports/
│   ├── Multiclass Sentiment Analysis of IMDb Reviews Using Modern NLP Methods.pdf
│   └── NLP.pdf
├── README.md
├── requirements.txt
└── .gitignore
```

## How to Run

Clone the repository:

```bash
git clone https://github.com/nhvunguyen02/final-project-multiclass-imdb-sentiment-analysis.git
cd final-project-multiclass-imdb-sentiment-analysis
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Open the notebook:

```bash
jupyter notebook notebooks/multiclass_imdb_sentiment_analysis.ipynb
```

Or upload the notebook to Google Colab and run it there.

## Reports

The final report and project idea document are available in the `reports/` directory.

## Authors

- Nguyen Hoang Vu Nguyen
- Nguyen Thuan Phat
- Nguyen Ngoc Duc
- Dinh Quang Duy
