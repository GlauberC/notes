# json-server

```sh
  yarn global add json-server
```

# server.json

- server.json

# api.js

- services/api.js

```sh
  yard add axios
```

```js
import axios from "axios";

const api = axios.create({
  baseURL: "http://localhost:3333"
});

export default api;
```

# Iniciar server.json

```sh
  json-server server.json -p 3333 -w
  sudo json-server --host 192.168.0.19 server.json -p 3333 -w
```
