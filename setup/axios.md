```sh
  yard add axios
```

- services/api.js

```js
import axios from "axios";

const api = axios.create({
  baseURL: "http://localhost:3333"
});

export default api;
```
