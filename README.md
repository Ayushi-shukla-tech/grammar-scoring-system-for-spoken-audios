# grammar-scoring-system-for-spoken-audios

## 1. Introduction

This project aims to develop an automated Grammar Scoring Engine that evaluates the grammatical quality of spoken language samples. The system takes audio recordings as input and assigns a grammar score on a scale from 0 to 5. This technology has applications in language assessment, educational technology, and speech analysis.

## 2. Dataset

The dataset consists of:
- 444 training audio samples with ground truth grammar scores
- 195 test audio samples for evaluation
- Each audio file is 45-60 seconds in length, stored in WAV format
- Scores follow a Likert scale from 0 to 5

## 3. Methodology

### 3.1 Audio Preprocessing
- Loaded audio files using librosa
- Resampled to 16kHz for standardization
- Applied silence trimming to focus on speech content
- Padded or truncated samples to ensure uniform length (60 seconds)

### 3.2 Feature Extraction
- Extracted Mel-Frequency Cepstral Coefficients (MFCCs) with 40 coefficients
- MFCCs capture the spectral characteristics of speech relevant to pronunciation and grammar
- Applied normalization to stabilize learning

### 3.3 Model Architecture
Implemented a hybrid CNN-LSTM architecture:
1. *CNN Layers*: Extract local acoustic features from the MFCC representations
   - Two convolutional layers with batch normalization
   - Max pooling for dimensionality reduction
   - Dropout for regularization

2. *Bidirectional LSTM*: Model temporal dependencies in speech
   - Captures long-range grammatical structures
   - Bidirectional to consider both past and future context

3. *Attention Mechanism*: Focus on the most relevant parts of speech
   - Helps the model attend to grammatical errors or well-formed structures
   - Provides interpretability by highlighting important time segments

4. *Fully Connected Layers*: Map learned representations to grammatical scores
   - Final sigmoid activation scaled to the 0-5 range

### 3.4 Training Pipeline
- Split training data into 80% training and 20% validation
- Used Mean Squared Error (MSE) as the loss function
- Adam optimizer with learning rate scheduling
- Early stopping based on validation loss
- Batch size of 16, trained for 30 epochs

## 4. Evaluation Metrics
- Root Mean Squared Error (RMSE)
- Mean Absolute Error (MAE)
- Distribution analysis of predicted scores

## 5. Conclusion
The Grammar Scoring Engine demonstrates the feasibility of automated grammar assessment from speech. The hybrid CNN-LSTM architecture with attention provides both accuracy and interpretability. This system can serve as a valuable tool for language assessment and learning applications.
