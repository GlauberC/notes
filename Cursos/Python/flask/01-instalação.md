## https://www.youtube.com/playlist?list=PLWhiA_CuQkbBhvPojHOPY81BmDt2eSfgI

```
sudo pip3 install Flask
```
## app.py
```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def index():
  return "index"

if __name__ == '__main__':
  app.run()
```