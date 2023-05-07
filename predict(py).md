```python

# predict.py

from flask import Flask, request, jsonify
from model import get_sentiment

app = Flask(__name__)

# Define API route for sentiment analysis
@app.route('/predict', methods=['POST'])
def predict():
    # Get text input from request body
    text = request.json['text']

    # Get sentiment prediction and probabilities
    sentiment, negative, neutral, positive = get_sentiment(text)

    # Return response as JSON
    response = {'sentiment': sentiment, 'negative': negative, 'neutral': neutral, 'positive': positive}
    return jsonify(response)

if __name__ == '__main__':
    app.run(debug=True)


```
