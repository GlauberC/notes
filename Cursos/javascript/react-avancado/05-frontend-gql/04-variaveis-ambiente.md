## Conteúdos

- create env variables

# create env variables

## .env.development

```
GRAPHQL_HOST='http://192.168.0.19:1337/graphql'
NEXT_PUBLIC_IMAGE_HOST='http://192.168.0.19:1337'

```

## src/utils/getImageUrl.ts

```ts
export const getImageUrl = (url: string) =>
  `${process.env.NEXT_PUBLIC_IMAGE_HOST}${url}`;
```

## src/components/Logo/index.tsx

```ts
import React from "react";
import * as S from "./styles";
import { LogoProps } from "types/api";
import { getImageUrl } from "utils/getImageUrl";

const Logo = ({ url, alternativeText }: LogoProps) => (
  <S.LogoWrapper src={getImageUrl(url)} alt={alternativeText} />
);

export default Logo;
```
