## Conteúdos

- Melhorando snapshots com o styled-components
- Editando Main

# Melhorando snapshots com o styled-components

```
yarn add jest-styled-components -D
```

## .jest/setup.ts

```ts
import "@testing-library/jest-dom";
import "jest-styled-components";
```

# Editando Main

## src/components/Main/index.tsx

```tsx
import * as S from "./styles";

const Main = () => (
  <S.Wrapper>
    <S.Logo
      src='/img/logo.svg'
      alt='Imagem de um átomo e React Avançado escrito ao lado.'
    />
    <S.Title>React Avançado</S.Title>
    <S.Description>
      Typescript, ReactJS, NextJS e Styled Components
    </S.Description>
    <S.Ilustration
      src='/img/hero-illustration.svg'
      alt='Um desenvolvedor de frente para uma tela com código'
    />
  </S.Wrapper>
);

export default Main;
```

## src/components/Main/styles.ts

```ts
import styled from "styled-components";

export const Wrapper = styled.main`
  background-color: #06092b;
  color: #fff;
  width: 100%;
  height: 100%;
  padding: 3rem;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
`;
export const Logo = styled.img`
  width: 25rem;
  margin-bottom: 2rem;
`;
export const Title = styled.h1`
  font-size: 2.5rem;
`;
export const Description = styled.h2`
  font-size: 2rem;
  font-weight: 400;
`;
export const Ilustration = styled.img`
  margin-top: 3rem;
  width: min(30rem, 100%);
`;
```

## src/components/Main/test.tsx

```tsx
import * as S from "./styles";

const Main = () => (
  <S.Wrapper>
    <S.Logo
      src='/img/logo.svg'
      alt='Imagem de um átomo e React Avançado escrito ao lado.'
    />
    <S.Title>React Avançado</S.Title>
    <S.Description>
      Typescript, ReactJS, NextJS e Styled Components
    </S.Description>
    <S.Ilustration
      src='/img/hero-illustration.svg'
      alt='Um desenvolvedor de frente para uma tela com código'
    />
  </S.Wrapper>
);

export default Main;
```
