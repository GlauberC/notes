## Conteúdos

- configurando types

# configurando types

## src/types/api.ts

```ts
export type LogoProps = {
  alternativeText: string;
  url: string;
};

export type LandingPageProps = {
  logo: LogoProps;
};
```

## src/pages/index.tsx

```ts
import React from "react";
import { GetStaticProps } from "next";

import SectionHero from "components/SectionHero";
import SectionAboutProject from "components/SectionAboutProject";
import SectionTech from "components/SectionTech";
import SectionConcepts from "components/SectionConcepts";
import SectionModules from "components/SectionModules";
import SectionAgenda from "components/SectionAgenda";
import PricingBox from "components/PricingBox";
import SectionAboutUs from "components/SectionAboutUs";
import SectionReviews from "components/SectionReviews";
import SectionFaq from "components/SectionFaq";
import Footer from "components/Footer";
import JsonSchema from "components/JsonSchema";
import { client } from "services/graphql/graphql";
import GET_LANDING_PAGE from "services/graphql/queries/getLandingPage";
import { LandingPageProps } from "types/api";

const Index = ({ logo }: LandingPageProps) => (
  <>
    <SectionHero logo={logo} />
    <SectionAboutProject />
    <SectionTech />
    <SectionConcepts />
    <SectionModules />
    <SectionAgenda />
    <PricingBox />
    <SectionAboutUs />
    <SectionReviews />
    <SectionFaq />
    <Footer />
    <JsonSchema />
  </>
);

export const getStaticProps: GetStaticProps = async () => {
  const { landingPage } = await client.request(GET_LANDING_PAGE);

  return {
    props: {
      ...landingPage,
    },
  };
};

export default Index;
```

## src/components/SectionHero/index.tsx

```ts
import React from "react";

import Logo from "components/Logo";
import Button from "components/Button";
import * as S from "./styles";

import { gaEvent } from "utils/ga";
import Container from "components/Container";
import { LogoProps } from "types/api";

type Props = {
  logo: LogoProps;
};

const onClick = () =>
  gaEvent({ action: "click", category: "cta", label: "hero button" });

const SectionHero = ({ logo }: Props) => (
  <S.Wrapper>
    <Container>
      <Logo {...logo} />

      <S.Content>
        <S.TextBlock>
          <S.Title>React Avançado</S.Title>
          <S.Description>
            Crie aplicações reais com NextJS, Strapi, GraphQL e mais!
          </S.Description>
          <S.ButtonWrapper>
            <Button
              href='https://www.udemy.com/course/react-avancado/?couponCode=PROMOSET20'
              onClick={onClick}
              wide
            >
              Comprar
            </Button>
          </S.ButtonWrapper>
        </S.TextBlock>

        <S.Image
          src='/img/hero-illustration.svg'
          alt='Ilustração de um desenvolvedor em frente a um computador com várias linhas de código.'
        />
      </S.Content>
    </Container>
  </S.Wrapper>
);

export default SectionHero;
```

## src/components/Logo/index.tsx

```ts
import React from "react";
import * as S from "./styles";
import { LogoProps } from "types/api";
import { BASE_URL } from "services/graphql/graphql";

const Logo = ({ url, alternativeText }: LogoProps) => (
  <S.LogoWrapper src={BASE_URL + url} alt={alternativeText} />
);

export default Logo;
```
