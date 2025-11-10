# lab4

## IV.1 – Setup and Configuration
- Prepared the working environment in Azure Databricks.
- Configured connection with Azure Data Lake Storage using the secure account key.
- Created and initialized a Spark session.
- Loaded the curated Gold dataset from Lab 3 (/gold/curated_reviews/).
- Selected essential columns: review_id, book_id, rating, and review_text.
- Verified that the dataset was correctly loaded and ready for feature engineering.

## IV.2 – Data Splitting and Preprocessing
- Split the curated dataset into train (70%), validation (15%), and test (15%) sets.
- Converted each split from Spark DataFrame to Pandas DataFrame for easier text handling.
- Applied text cleaning by converting all text to lowercase.
- Added basic text statistics such as:
- Number of words (review_length_words).
- Number of characters (review_length_chars).
- These steps helped prepare the data for advanced text feature extraction.

## IV.3 – Feature Engineering
- Generated multiple groups of textual features:
- Basic Features:
  * Word count and character count of each review.
  * Sentiment Features:
  * Used VADER Sentiment Analyzer (NLTK) to calculate:
  * Positive (sentiment_pos)
  * Negative (sentiment_neg)
  * Neutral (sentiment_neu)
  * Compound (sentiment_compound) scores.

## TF-IDF Features:
- Applied TF-IDF vectorization to represent text numerically.
- Generated around 5,000 features showing word importance across reviews.
- Semantic Embeddings:
   * Used Sentence-BERT (all-MiniLM-L6-v2) to extract 384 contextual embeddings per review.
   * These embeddings captured deep semantic meaning in the text.
- Bonus Feature:
   * Added an average word length column for additional linguistic insight.
   * Combined all feature groups to form a comprehensive feature set.

## IV.4 – Combined Feature Set and Output
- Merged all engineered features with original metadata (review ID, book ID, rating).
- Created one final DataFrame that included:
- Metadata
- Basic features
- Sentiment features
- TF-IDF features
- BERT embeddings
- Bonus feature
- Saved the final feature dataset in the Gold layer under:
abfss://lakehouse@goodreadsreviews60104384.dfs.core.windows.net/gold/features_v2/train/
- Used the Delta format with schema merging to maintain structure and compatibility.
- Conducted a full verification to ensure that all feature groups were included successfully.

## Final Verification and Completion
- Confirmed presence of:
Metadata → OK
Basic features → OK
Sentiment features → OK
TF-IDF (~5000) → OK (4966 found)
Embeddings (~384) → OK (384 found)
Bonus feature → OK
Verified correct number of rows (10869).
Small data type differences (int vs bigint) inherited from Lab 3 were acceptable.

All parts of Lab 4 were successfully completed.

Produced a clean, feature-rich dataset ready for machine learning model training in upcoming labs.
