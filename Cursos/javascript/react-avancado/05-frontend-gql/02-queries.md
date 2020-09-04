## Conteúdos

- first query
- config and import

# first query

## src/services/graphql/queries/getLandingPage.ts

```ts
import { gql } from "graphql-request";

const GET_LANDING_PAGE = gql`
  query {
    landingPage {
      logo {
        url
        alternativeText
      }
    }
  }
`;
export default GET_LANDING_PAGE;
```

# config and import

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

const Index = () => (
  <>
    <SectionHero />
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

  console.log(landingPage);

  return {
    props: {
      ...landingPage,
    },
  };
};

export default Index;
```
