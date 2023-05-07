```python

# model.py

import torch
from transformers import AutoTokenizer, AutoModelForSequenceClassification

# Load tokenizer and model
tokenizer = AutoTokenizer.from_pretrained('cardiffnlp/twitter-roberta-base-sentiment')
model = AutoModelForSequenceClassification.from_pretrained('cardiffnlp/twitter-roberta-base-sentiment')

# Define possible sentiment labels
labels = ['negative', 'neutral', 'positive']

# Define function for predicting sentiment of a text input
def get_sentiment(text):
    # Tokenize input text and truncate if necessary
    inputs = tokenizer(text, padding='max_length', truncation=True, max_length=512, return_tensors='pt')

    # Get model predictions and softmax probabilities
    outputs = model(**inputs)
    logits = outputs.logits
    probs = torch.softmax(logits, dim=1).detach().numpy()[0]

    # Get predicted sentiment label
    sentiment = labels[probs.argmax()]

    # Return sentiment label and probabilities for each label
    return sentiment, probs[0]*100, probs[1]*100, probs[2]*100

```
