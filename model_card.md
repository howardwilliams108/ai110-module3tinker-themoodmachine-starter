# Model Card: Mood Machine

This model card is for the Mood Machine project, which includes **two** versions of a mood classifier:

1. A **rule based model** implemented in `mood_analyzer.py`
2. A **machine learning model** implemented in `ml_experiments.py` using scikit learn

You may complete this model card for whichever version you used, or compare both if you explored them.

## 1. Model Overview

**Model type:**  
  
I used both the rule-based model in mood_analyzer.py and the machine-learning model in ml_experiments.py and I compared both models

**Intended purpose:**  
What is this model trying to do?  
The mood Machine analyzes the short text messages and predicts whether they are negative, positive, neutral, or mixed.
**How it works (brief):**  
For the rule based version, describe the scoring rules you created.  
The rule-based model searches for positive and negative words and then calculating a sentiment score. The machine-learning model learns patterns from labeled examples to predict sentiment.



## 2. Data

**Dataset description:**  

The dataset contains eleven (11) posts in SAMPLE_POSTS; I added five new posts to the original six.

**Labeling process:**  
  
I assigned labels based on the intended sentiment of each post. Some examples were difficult to label because they contained sarcasm or neutral emotions.

**Important characteristics of your dataset:**  
Examples you might include:  

- Contains positive, negative, neutral, and mixed sentiments. 
- Includes sarcasm, such as "Great, my PC CRASHED!"  
- Contains short messages about everyday experiences  


**Possible issues with the dataset:**  
 It does not represent every type of slang, emoji, writing style, or cultural expression making the dataset is small and having limited language variation.

## 3. How the Rule Based Model Works (if used)

**Your scoring rules:**  
  
The preprocess() method converts text to lowercase, removes punctuation, and separates sentences into words.

The score_text() method adds one point for positive words and subtracts one point for negative words.

I implemented negation handling so words such as "not," to reverse the sentiment of the following word.

I also added "fire" to the positive word list to recognize slang.

The predict_label() method returns positive for scores above zero, negative for scores below zero, and neutral for scores equal to zero.

**Strengths of this approach:**  
The rule-based model is simple, fast, and easy to understand.

**Weaknesses of this approach:**  
The model struggles with sarcasm, mixed emotions, and context.

For example, adding "fire" helped classify "This game is fire" as positive, but I noticedit also classified "The building is on fire" as positive.

## 4. How the ML Model Works (if used)

**Features used:**  
The machine-learning model uses scikit-learn and CountVectorizer to represent text as numerical word-frequency features.

**Training data:**  
The model was trained using SAMPLE_POSTS and TRUE_LABELS from dataset.py.

**Training behavior:**  

The machine-learning model was evaluated on the same dataset used for training, so this does not demonstrate its accuracy on new data.

**Strengths and weaknesses:**  
The machine-learning model learned patterns from the labeled examples and correctly classified all 11 training posts. However, it struggled with some unfamiliar sentences and could not always interpret sarcasm or context correctly.

## 5. Evaluation

**How you evaluated the model:**  
I ran python main.py to evaluate the rule-based classifier and python ml_experiments.py to evaluate the machine-learning classifier.

**Examples of correct predictions:**  
- "I love this class so much" was correctly classified as positive by both models.

- "Today was a terrible day" was correctly classified as negative by both models.

**Examples of incorrect predictions:**  
- "Feeling tired but kind of hopeful" was classified as negative by the rule-based model instead of mixed.
- "Great, my PC CRASHED!" was classified as positive by the rule-based model instead of negative.

For the rule-based model and machine-learning model interpreted "I love getting stuck in traffic" as positive, missing the likely sarcasm.

## 6. Limitations



- The dataset is small limiting how well the the models can recognize different language styles
- The ML classifier can learn patterns from data, but it may make incorrect predictions when given sentences different from its training examples. 
- It cannot detect sarcasm reliably  


## 7. Ethical Considerations

- Mood detection systems can make incorrect predictions about people's emotions. This could be harmful if used to evaluate personal messages or identify emotional distress.
- People using informal or regional expressions may receive less accurate predictions for example the rule-based model initially failed to recognize the slang expression "This game is fire."
- I used AI assistance for this assignment but AI recommendations need to be tested instead of being just accepted because AI's suggestion of adding "fire: improved slang recognition but caused another incorrect prediction involving a building fire. 

## 8. Ideas for Improvement

- List ways to improve either model.  
- Improve the detection of mixed emotions and sarcasm.
- Improve how the classifier processes emojis and slang.
- Expanding the dataset with more unique posts.
