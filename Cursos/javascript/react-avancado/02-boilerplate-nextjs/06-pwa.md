## Conteúdos

- install and configure

# install and configure

```
yarn add next-pwa
```

## next.config.js

```js
// eslint-disable-next-line @typescript-eslint/no-var-requires
const withPWA = require("next-pwa");
const isProd = process.env.NODE_ENV === "production";

module.exports = withPWA({
  pwa: {
    dest: "public",
    disable: !isProd,
  },
});
```

## public/manifest.json

```js
{
  "name": "React Avançado - Boilerplate",
  "short_name": "React Avançado",
  "icons": [
    {
      "src": "/img/icon-192.png",
      "type": "image/png",
      "sizes": "192x192"
    },
    {
      "src": "/img/icon-512.png",
      "type": "image/png",
      "sizes": "512x512"
    }
  ],
  "background_color": "#06092B",
  "description": "Boilerlate utilizando Typescript, React, NextJS e Styled Components!",
  "display": "fullscreen",
  "start_url": "/",
  "theme_color": "#06092B"
}

```

## src/pages/\_app.tsx

```js
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
        <link rel='manifest' href='manifest.json' />
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

```
NODE_ENV=production yarn build
```
