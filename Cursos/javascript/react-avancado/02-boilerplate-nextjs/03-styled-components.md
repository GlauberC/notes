## Conteúdos

- install
- styled

# install

```
yarn add babel-plugin-styled-components @types/styled-components -D
yarn add styled-components
```

## .babelrc

```json
{
  "plugins": [
    [
      "babel-plugin-styled-components",
      {
        "ssr": true
      }
    ]
  ],
  "presets": ["next/babel", "@babel/preset-typescript"]
}
```

## src/pages/\_document.tsx

- https://github.com/vercel/next.js/blob/master/examples/with-styled-components/pages/_document.js

```tsx
import Document, { DocumentContext } from "next/document";
import { ServerStyleSheet } from "styled-components";

export default class MyDocument extends Document {
  static async getInitialProps(ctx: DocumentContext) {
    const sheet = new ServerStyleSheet();
    const originalRenderPage = ctx.renderPage;

    try {
      ctx.renderPage = () =>
        originalRenderPage({
          enhanceApp: (App) => (props) =>
            sheet.collectStyles(<App {...props} />),
        });

      const initialProps = await Document.getInitialProps(ctx);
      return {
        ...initialProps,
        styles: (
          <>
            {initialProps.styles}
            {sheet.getStyleElement()}
          </>
        ),
      };
    } finally {
      sheet.seal();
    }
  }
  render() {
    return (
      <Html lang='pt-BR'>
        <Head />
        <body>
          <Main />
          <NextScript />
        </body>
      </Html>
    );
  }
}
```

# styled

## src/styles/global.ts

```css
import { createGlobalStyle } from "styled-components";

const GlobalStyles = createGlobalStyle`
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box
}
html{
  font-size: 62.5%
}
html, body, #__next{
  height: 100%;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif
}
`;

export default GlobalStyles;
```

## tsconfig.json

```json
{
  "compilerOptions": {
    "baseUrl": "src",
    ...
  },
,..
}

```

## src/pages/\_app.tsx

```ts
import GlobalStyles from "styles/global";
import { AppProps } from "next/app";
import Head from "next/head";

function App({ Component, pageProps }: AppProps) {
  return (
    <>
      <Head>
        <title>React Avançado - Boilerplate</title>
        <link rel='shortcut icon' href='/img/icon-512.png' />
        <link rel='apple-touch-icon' href='/img/icon-512.png' />
        <meta
          name='description'
          content='A simple project starter to work with Typescript, React, NextJS and Styled Components'
        />
      </Head>
      <GlobalStyles />
      <Component {...pageProps} />
    </>
  );
}

export default App;
```

## src/pages/index.tsx

```ts
import Main from "components/Main";

export default function Home() {
  return <Main />;
}
```
