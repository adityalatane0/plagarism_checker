# Text Similarity & Plagiarism Detection

This project implements a system for analyzing text similarity and potentially detecting plagiarism by extracting various linguistic and semantic features from pairs of text documents and using a simple neural network classifier.

## Features

The project calculates the following features for each pair of texts to quantify their similarity and complexity difference:

*   **Cosine TF-IDF Similarity:** Measures the similarity between texts based on their TF-IDF vector representations.
*   **Cosine Embedding Similarity:** Measures semantic similarity using embeddings generated by a Sentence Transformer model.
*   **N-gram Overlap:** Quantifies the common n-grams (sequences of n words) between texts (using trigrams by default).
*   **POS Tag Difference:** Calculates the difference in the distribution of Parts-of-Speech tags between texts.
*   **Average Sentence Length Difference:** The absolute difference between the average sentence lengths of the two texts.
*   **Vocabulary Richness Difference:** The absolute difference between the lexical diversity (type-token ratio) of the two texts.
*   **Longest Common Subsequence (LCS) Ratio:** Measures the ratio of the length of the longest common subsequence (character-based during training, word-based in prediction function example) to the length of the longer text.
*   **Readability Difference:** The absolute difference between the Flesch Reading Ease scores of the two texts.

These features are then used to train a model to classify the relationship between the text pairs (e.g., as potentially plagiarized/similar or not).

## Setup and Installation

1.  **Clone the Repository:**
    ```bash
    git clone <repository_url>
    cd <repository_folder>
    ```

2.  **Install Dependencies:** Install the required Python packages. It's recommended to use a virtual environment.
    ```bash
    pip install -r requirements.txt
    ```
    *(Create a `requirements.txt` file containing the following:)*
    ```
    pandas
    numpy
    nltk
    spacy
    sentence-transformers
    textstat
    scikit-learn
    torch
    torchvision
    tqdm
    ```

3.  **Download NLTK Data:**
    ```python
    import nltk
    nltk.download('punkt')
    nltk.download('averaged_perceptron_tagger')
    nltk.download('stopwords')
    nltk.download('punkt_tab') # May not be strictly necessary depending on NLTK version
    nltk.download('averaged_perceptron_tagger_eng') # May not be strictly necessary
    ```
    You can run these lines in a Python interpreter or add them to the beginning of your main script.

4.  **Download SpaCy Model:**
    ```bash
    python -m spacy download en_core_web_sm
    ```

## Data

The project expects an input file named `train_snli.txt` in a directory accessible at `/content/`. This file should be tab-separated and contain at least three columns: `text1`, `text2`, and `label`. **Crucially, for the training part of the provided code to work with the `BCELoss` and `Sigmoid` output, the `label` column in this input file is expected to be binary (0 or 1).**

The script will perform the following data steps:
1.  Convert `train_snli.txt` to `ft.csv`.
2.  Read the first 20,000 rows from `ft.csv`.
3.  Extract the features listed above and save them to `plagiarism_features.csv`.

## Usage

The provided code combines data preparation, feature extraction, model training, and prediction. You can save the code into a Python file (e.g., `plagiarism_detector.py`) and run it.

```bash
python plagiarism_detector.py
