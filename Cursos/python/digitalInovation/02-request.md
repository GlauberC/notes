## src/app.py
```py
from flask import Flask, jsonify, request
import json

app = Flask(__name__)

@app.route('/people/<int:id>')
def people(id):
  return jsonify({"id": id, "name": "Glauber", "job": "developer"})

# @app.route('/soma/<int:valor1>/<int:valor2>/')
# def soma(valor1, valor2):
  # return jsonify({"soma": valor1 + valor2})

@app.route('/soma', methods=['POST', 'GET'])
def soma():
  if request.method == 'POST':
    data = json.loads(request.data)

    total = sum(data['valores'])
    return jsonify({"soma": total})

if __name__ == "__main__":
    app.run(debug=True)
```