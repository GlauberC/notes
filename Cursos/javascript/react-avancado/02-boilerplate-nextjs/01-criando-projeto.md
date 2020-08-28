## Conteúdos
- Documentação
  - https://nextjs.org/docs
- Install
- Typescript
- Move pages to src
- Rename js to ts e tsx
- Configurando editor config
- eslint
- prettier
- git husky

# Install
 ```
 yarn create next-app
 ```

# Typescript
```
touch tsconfig.json

yarn dev

yarn add --dev typescript @types/react @types/node

yarn dev
``` 

# tsconfig.json
```json
...
"strict": true,
...
```

# Configurando editor config
## .editorconfig
```
root = true

[*]
end_of_line = lf
indent_style = space
indent_size = 2
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

# eslint
```
yarn add eslint -D
yarn eslint --init
yarn add eslint-plugin-react-hooks -D
```

## .eslintrc.json
```json
{
  "env": {
    "browser": true,
    "es2020": true
  },
  "settings": {
    "react": {
      "version": "detect"
    }
  },
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:@typescript-eslint/recommended"
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

## package.json
```json
  "scripts": {
    ...
    "lint": "eslint src"
    ...
  },
```

# prettier
```
yarn add prettier eslint-config-prettier eslint-plugin-prettier -D
```
## .prettierrc
```json
{
  "trailingComma": "none",
  "semi": false,
  "singleQuote": true
}

```

## .eslintrc.json
```json
{
  "env": {
    "browser": true,
    "es2020": true
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

# git husky
```
yarn add husky lint-staged -D 
```

## package.json
```json
{

  "scripts": {
    ...
    "lint": "eslint src --max-warnings=0"
  },
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "src/**/*": [
      "yarn lint --fix"
    ]
  },
  ...
}

```