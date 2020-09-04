## Conteúdos

- repository
  - https://github.com/React-Avancado/landing-page
- install graphql
- configurando client

# install graphql

```
yarn add graphql graphql-request
```

# configurando client

## src/services/graphql/graphql.ts

```ts
import { GraphQLClient } from "graphql-request";

export const BASE_URL = "http://localhost:1337";

export const client = new GraphQLClient(`${BASE_URL}/graphql`);
```
