## Conteúdos

- configure storybook

# configure storybook

- https://storybook.js.org/docs/react/get-started/install

```
npx sb init
```

- Delete stories dir

## package.json

```json
{
    "scripts": {
      ...
    "storybook": "start-storybook -s ./public -p 6006",
    "build-storybook": "build-storybook -s ./public"
    ...
  },
}
```

## .storybook/main.js

```js
module.exports = {
  stories: ["../src/components/**/stories.@(js|jsx|ts|tsx)"],
  addons: ["@storybook/addon-links", "@storybook/addon-essentials"],
};
```

## .storybook/preview.js

```js
import GlobalStyles from "../src/styles/global";

export const decorators = [
  (Story) => (
    <>
      <GlobalStyles />
      <Story />
    </>
  ),
];
```

## src/components/Main/stories.tsx

```tsx
import { Story, Meta } from "@storybook/react/types-6-0";

import Main from ".";
export default {
  title: "Main",
  component: Main,
} as Meta;

export const Basic: Story = (args) => <Main {...args} />;
```

## src/components/Main/index.tsx

```tsx
import * as S from "./styles";

const Main = ({
  title = "React Avançado",
  description = "Typescript, ReactJS, NextJS e Styled Components",
}) => (
  <S.Wrapper>
    <S.Logo
      src='/img/logo.svg'
      alt='Imagem de um átomo e React Avançado escrito ao lado.'
    />
    <S.Title>{title}</S.Title>
    <S.Description>{description}</S.Description>
    <S.Ilustration
      src='/img/hero-illustration.svg'
      alt='Um desenvolvedor de frente para uma tela com código'
    />
  </S.Wrapper>
);

export default Main;
```
