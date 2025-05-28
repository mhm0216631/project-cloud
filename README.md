from flask import Flask, jsonify
from pyngrok import ngrok
import threading
import json

app = Flask(__name__)

@app.route("/")
def home():
    return "✅ News Sentiment Classifier is Live!"

@app.route("/news")
def news():
    with open("articles_json.json", "r") as f:
        data = json.load(f)
    return jsonify(data)

def run():
    app.run(port=5000)

threading.Thread(target=run).start()

print("Public URL:", ngrok.connect(5000))
