## Conteúdos
- param no url

## app.py
```python
from flask import Flask
app = Flask(__name__)

@app.route("/hello/<nome>")
def hello(nome):
  return "<h1>oi {}</h1>".format(nome)

@app.route('/blog/<int:postID>')
def blog(postID): 
    return "blog info {}".format(postID)

if __name__ == '__main__':
  app.run(debug=True, port="3334")
```