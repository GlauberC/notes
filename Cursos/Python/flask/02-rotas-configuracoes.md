## Conteúdos
- debug
- port
- routes

## app.py
```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def index():
  return "index"

def teste():
  return "<p>Testaaaando</p>"

app.add_url_rule("/teste", "teste", teste)

if __name__ == '__main__':
  app.run(debug=True, port="3334")
```