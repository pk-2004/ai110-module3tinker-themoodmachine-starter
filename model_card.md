# Model Card: Mood Machine

This model card is for the Mood Machine project, which includes **two** versions of a mood classifier:

1. A **rule based model** implemented in `mood_analyzer.py`
2. A **machine learning model** implemented in `ml_experiments.py` using scikit learn

You may complete this model card for whichever version you used, or compare both if you explored them.

## 1. Model Overview

**Model type:**  
Describe whether you used the rule based model, the ML model, or both.  
Example: “I used the rule based model only” or “I compared both models.”

I used the rule based model but compared it with the ML model. 

**Intended purpose:**  
What is this model trying to do?  
Example: classify short text messages as moods like positive, negative, neutral, or mixed.

The rule based model assigns a higher score for postive words and subtracts from the score for negative words. 

**How it works (brief):**  
For the rule based version, describe the scoring rules you created.  
For the ML version, describe how training works at a high level (no math needed).

The rule based version goes through each token and adds points if the word is positive. If it is a stronger positve, more points are added and same concept for negative points. For sarcasm, it is checked wheter the sentence has both a postive and negative signal to accordingly adjust the score. Baesed on the score, a label is assigned

The ML based model relies on logistical regression and the weights are updated for each iteration to ensure the model accuracy improves. 

## 2. Data

**Dataset description:**  
Summarize how many posts are in `SAMPLE_POSTS` and how you added new ones.

There are 15 sample posts. I add news ones as I think of harder examples which I believe the algorithm might struggle with. 

**Labeling process:**  
Explain how you chose labels for your new examples.  
Mention any posts that were hard to label or could have multiple valid labels.

For sentences that had overwhelming positive or negative words, classification was easy. However, for sentence with a tone like while negative, it felt a little postive, it was hard to categorize wheter it was neutral or more towards the postive side. 
**Important characteristics of your dataset:**  
Examples you might include:  

- Contains slang or emojis  
- Includes sarcasm  
- Some posts express mixed feelings  
- Contains short or ambiguous messages

Has some sarcasm and some long and complex sentence with a mix of positive and negative signal words. 

**Possible issues with the dataset:**  
Think about imbalance, ambiguity, or missing kinds of language.


Maybe more negative examples than positives. Less training sentence with emojis. Error in human labelling. 

## 3. How the Rule Based Model Works (if used)

**Your scoring rules:**  
Describe the modeling choices you made.  
Examples:  

- How positive and negative words affect score  
- Negation rules you added  
- Weighted words  
- Emoji handling  
- Threshold decisions for labels

Added a list with stronger positive and negative words and gave higher weights accordingly. I used method of adding score for postive words and subtrating for negative words. 

**Strengths of this approach:**  
Where does it behave predictably or reasonably well?

Obvious cases. 

**Weaknesses of this approach:**  
Where does it fail?  
Examples: sarcasm, subtlety, mixed moods, unfamiliar slang.

I guess examples with both negative and postive examples, as it could have sarcasm, which in reality can make a sentence postive or negative. 

## 4. How the ML Model Works (if used)

**Features used:**  
Describe the representation.  
Example: “Bag of words using CountVectorizer.”

**Training data:**  
State that the model trained on `SAMPLE_POSTS` and `TRUE_LABELS`.

**Training behavior:**  
Did you observe changes in accuracy when you added more examples or changed labels?

**Strengths and weaknesses:**  
Strengths might include learning patterns automatically.  
Weaknesses might include overfitting to the training data or picking up spurious cues.

## 5. Evaluation

**How you evaluated the model:**  
Both versions can be evaluated on the labeled posts in `dataset.py`.  
Describe what accuracy you observed.

Got 67 percent accuracy

**Examples of correct predictions:**  
Provide 2 or 3 examples and explain why they were correct.

"it is what it is 🥲" -> negative
"missing my friends so much rn 😢" -> negative   

**Examples of incorrect predictions:**  
Provide 2 or 3 examples and explain why the model made a mistake.  
If you used both models, show how their failures differed.

"lowkey stressed but highkey thriving rn" -> negative

"Feeling tired but kind of hopeful" -> negative     

## 6. Limitations

Describe the most important limitations.  
Examples:  

- The dataset is small  
- The model does not generalize to longer posts  
- It cannot detect sarcasm reliably  
- It depends heavily on the words you chose or labeled


The model is not that great in classifying sentences as neutral. 
## 7. Ethical Considerations

Discuss any potential impacts of using mood detection in real applications.  
Examples: 

- Misclassifying a message expressing distress  
- Misinterpreting mood for certain language communities  
- Privacy considerations if analyzing personal messages


Human labelers can label sentences differently
Some sentences may not be used as often in real life


## 8. Ideas for Improvement

List ways to improve either model.  
Possible directions:  

- Add more labeled data  
- Use TF IDF instead of CountVectorizer  
- Add better preprocessing for emojis or slang  
- Use a small neural network or transformer model  
- Improve the rule based scoring method  
- Add a real test set instead of training accuracy only


Add more data, ensure class balance
more emoji representation
add some additional comnplexity to rule scoring method, especaillay for classifying mixed signals
Use different ML model like random forest. 