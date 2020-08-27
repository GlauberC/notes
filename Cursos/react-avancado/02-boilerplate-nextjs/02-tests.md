## Conteúdos

- install and configuration jest
- configure react testing library
- test

# install and configuration jest

```
yarn add jest babel-jest @babel/core @babel/preset-env @babel/preset-typescript @types/jest -D
```

## .eslintrc.json

```json
{
  "env": {
    "browser": true,
    "es2020": true,
    "jest": true,
    "node": true
  },
  "settings": {
    "react": {
      "version": "detect"
    }
  },
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:prettier/recommended"
  ],
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaFeatures": {
      "jsx": true
    },
    "ecmaVersion": 12,
    "sourceType": "module"
  },
  "plugins": ["react", "@typescript-eslint", "react-hooks"],
  "rules": {
    "react/react-in-jsx-scope": "off",
    "react-hooks/rules-of-hooks": "error",
    "react-hooks/exhaustive-deps": "warn",
    "react/prop-types": "off",
    "@typescript-eslint/explicit": "off",
    "@typescript-eslint/explicit-module-boundary-types": "off"
  }
}
```

## jest.config.js

```js
module.exports = {
  testEnvironment: "jsdom",
  testPathIgnorePatterns: ["/node_modules/", "/.next/"],
  collectCoverage: true,
  collectCoverageFrom: ["src/**/*.ts(x)"],
  setupFilesAfterEnv: ["<rootDir>/.jest/setup.ts"],
};
```

## .babelrc

```json
{
  "presets": ["next/babel", "@babel/preset-typescript"]
}
```

## .jest/setup.ts

## package.json

```json
{
  "scripts": {
    ...
    "test": "jest",
    "test:watch": "yarn test --watch"
  },
  "lint-staged": {
    "src/**/*": [
      ...
      "yarn test --findRelatedTests --bail"
    ]
  },
}
```

# configure react testing library

```
yarn add @testing-library/react @testing-library/jest-dom -D
```

## .jest/setup.ts

```ts
import "@testing-library/jest-dom";
```

# test

## src/components/Main/index.tsx

```ts
const Main = () => (
  <main>
    <h1>React Avançado</h1>
  </main>
);

export default Main;
```

## src/components/Main/test.tsx

```ts
import { render, screen } from "@testing-library/react";

import Main from ".";

describe("<Main/>", () => {
  it("should render the heading", () => {
    const { container } = render(<Main />);

    expect(
      screen.getByRole("heading", { name: /react avançado/i })
    ).toBeInTheDocument();

    expect(container.firstChild).toMatchSnapshot();
  });
});
```

- https://testing-library.com/docs/react-testing-library/cheatsheet
