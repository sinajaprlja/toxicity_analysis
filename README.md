# Toxicity Analysis of Reddit Posts

This project uses a pretrained **RoBERTa model** to analyze and classify toxicity in Reddit comments. It is part of an effort to understand patterns of toxic language across different subreddit categories.


## Data Loading and Preprocessing <br>
#### Data Sampling
- Analyzed a **10% random sample** of the original dataset
- Used **stratified sampling** to maintain:
  - Original subreddit category proportions
  - Balance between short/long posts
- Ensures representative results while improving processing speed
- Relevant data is extracted and preprocessed in: [load_and_preprocess.ipynb](https://github.com/sinajaprlja/toxicity_analysis/blob/main/src/load_and_preprocess.ipynb). 
#### Model Used: 
A **fine-tuned RoBERTa model** from **Hugging Face** for toxicity detection: [s-nlp/roberta_toxicity_classifier](https://huggingface.co/s-nlp/roberta_toxicity_classifier)


## Analysis <br>

### Key Findings (from [analysis.ipynb](https://github.com/sinajaprlja/toxicity_analysis/blob/main/src/analysis.ipynb))

#### Toxicity Distribution
- **95.8%** of comments were classified as **non-toxic**, while **4.2%** were toxic.
- **Bootstrapping** revealed:
  - The subreddit category **"tifu"** was the **most toxic**
  - **"offmychest"** and **"pettyrevenge"** also showed high toxicity (their lower confidence bounds exceeded other categories)

### Hypothesis Testing

#### 1. Differences in toxicity between subreddit categories? **Yes** 
- Extremely low p-value (< 0.05) confirms significant differences

#### 2. Are longer posts less toxic than shorter ones? **Yes**  
- Data violated normality assumptions (tested with: log, square root, Box-Cox, and Yeo-Johnson transformations)
- **Mann-Whitney U-Test** results:
  - p-value < 0.05 → statistically significant
  - Reject null hypothesis: word counts differ between toxic/non-toxic posts
