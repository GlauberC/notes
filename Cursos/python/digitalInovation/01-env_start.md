## Conteúdos
- Criação da env
- Instalação do flask
- Iniciando aplicação 


### Criação da env
```
virtualenv -p python3 envDigIno

. envDigIno/bin/activate

which python

deactivate
```
### Instalação do flask
```
pip3 install Flask

pip3 freeze
```
### Instalação do flask

## run.py
```py
from flask import Flask

app = Flask(__name__)

@app.route('/<int:numero>')
def hello(numero):
  return 'Ola mundo. {}'.format(numero)

if __name__== "__main__":
  app.run(debug=True) # debug: auto restart
```

