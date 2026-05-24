# Dataset

This project uses movie review datasets for multiclass sentiment analysis.

## Data Sources

The final dataset is built from two main sources:

1. IMDb movie reviews
   - Positive and negative movie reviews
   - Original binary sentiment labels
   - Used for Negative and Positive classes

2. Neutral movie reviews
   - Neutral reviews originally collected in Russian
   - Translated into English
   - Used for the Neutral class

## Label Mapping

```text
0 = Negative
1 = Neutral
2 = Positive
```

## Expected Files

The original and processed datasets are not included in this repository due to file size and distribution constraints.

Expected local structure:

```text
data/
├── raw/
│   ├── IMDB Dataset.csv
│   └── Dataset_Tieng_Nga.zip
├── processed/
│   ├── pos_neg_data.csv
│   ├── neutral_data.csv
│   ├── final_combined_data.csv
│   ├── train_data.csv
│   ├── val_data.csv
│   └── test_data.csv
```

## Notes

The notebook can either download the processed CSV files from Google Drive or read them from the local `data/processed/` directory.

The dataset is excluded from Git tracking to keep the repository lightweight.