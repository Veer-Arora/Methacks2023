``` html

<!DOCTYPE html>
<html>
<head>
    <title>Sentiment Analysis App</title>
    <link rel="stylesheet" type="text/css" href="{{ url_for('static', filename='css/styles.css') }}">
</head>
<body>
    <h1>Sentiment Analysis App</h1>
    <form method="POST" action="{{ url_for('predict') }}">
        <label for="text">Enter Text:</label>
        <input type="text" name="text" id="text">
        <button type="submit">Analyze</button>
    </form>
    <div id="results">
        {% if results %}
            <h2>Results:</h2>
            <p>Positive: {{ results['positive'] }}</p>
            <p>Negative: {{ results['negative'] }}</p>
            <p>Neutral: {{ results['neutral'] }}</p>
        {% endif %}
    </div>
</body>
</html>


```
