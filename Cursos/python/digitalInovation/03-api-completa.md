
```
pip3 install flask_api
```

## src/app.py
```py
from flask import Flask, jsonify, request
from flask_api import status
import json
import uuid

app = Flask(__name__)

devs_list = []

@app.route("/devs", methods=["POST", "GET"])
def devs():
  try:
    if request.method == "POST":
      data = json.loads(request.data)
      data['id'] = uuid.uuid4()
      devs_list.append(data)
      return data
    elif request.method == "GET":
      return jsonify(devs_list)
  except Exception:
    return jsonify({'status': 'error', 'data': 'There is an internal error'}), status.HTTP_500_INTERNAL_SERVER_ERROR

@app.route("/devs/<int:pos>", methods=["GET", "PUT", "DELETE"])
def devsParam(pos):
  try:
    if(request.method == "GET"):
      return jsonify(devs_list[pos])

    elif request.method == "DELETE":
      user = jsonify(devs_list[pos])
      del devs_list[pos]
      return user

    elif request.method == "PUT":
      data = json.loads(request.data)
      user = devs_list[pos]
      user['name'] = data['name']
      user['skills'] = data['skills']
      devs_list[pos] = user
      return jsonify(user)
  except IndexError:
    response = {'status': 'error', 'data': 'There is no developer in this position'}
    return jsonify(response), status.HTTP_404_NOT_FOUND
  except Exception:
      return jsonify({'status': 'error', 'data': 'There is an internal error'}), status.HTTP_500_INTERNAL_SERVER_ERROR
  

if __name__ == "__main__":
    app.run(debug=True)
```