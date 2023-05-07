``` python


import sys
sys.path.append('C:/Users/Veer/Documents/VSCode Files/Sentiment Analysis Program')

from flask import Flask, render_template, request
from Backend.model import get_sentiment

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/predict', methods=['POST'])
def predict():
    text = request.form['text']
    sentiment, negative, neutral, positive = get_sentiment(text)
    results = {'sentiment': sentiment, 
               'negative': f'{negative:.2f}%',
               'neutral': f'{neutral:.2f}%',
               'positive': f'{positive:.2f}%'}
    return render_template('index.html', results=results)

if __name__ == '__main__':
    app.run(debug=True)

```
