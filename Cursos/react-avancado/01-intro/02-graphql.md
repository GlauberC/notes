Linguagem de consulta de dados desenvolvida e usada pelo Facebook desde 2012

# Dificuldades na Rest API
- Dificuldades para evoluir a API (criação de N versões)
- Entrega de dados nem sempre necessários
- Aumento no tamanho da requisição
- Rotas altamente acopladas

# Vantagens do GraphQL
- Permite evolução constante
- Entrega somente dados requisitados (tamanho menor e mais rápido)
- Rota única, dados altamente desacoplados
  

# Exemplos de query
- https://developer.github.com/v4/explorer/
```js
query {
  user(login: "glauberc"){
    avatarUrl
    bio
    followers{
      totalCount
    }
  }
}
```

# GraphQL Clients
- São responsáveis por criar camadas de abstração para realizar queries/mutations, sistemas de cache, validações e otimizações
- Fetch Client x Caching Client
- Clients mais usados
  - FetchQL
  - GraphQL Request
  - uRQL
  - Relay Modern
  - Apollo Client

# FetchQL
## Vantagens
- Bastante leve
- API simplificada
- Escrito com ES2015 e modules
- Isomórfico (Node/Browser)

## Desvantagens
- Não possui sistema de cache
- Não possui tratamento de dados e validações
- Não tem contexto de estados


# GraphQL Request
## Vantagens
- Super simples e leve
- Baseado em promises (async/await)
- Suporte a Typescript
- isomórfico 

## Desvantagens
- Não possui sistema de cache
- Não possui tratamento de dados e validações
- Não tem contexto de estados

# uRQL
## Vantagens
- Bastante leve e focado em performance
- Altamente extensível
- Junto com Exchanges possui caching
- possui suporte offline

## Desvantagens
- Biblioteca bastante nova (poucos materiais sobre)
- Pouca adoção ainda


# Relay Modern
## Vantagens
- Focado em performance
- Pré-compila as queries do GraphQL em build time (evita que o usuário baixe o parser)
- Possui sistema de caching/states

## Desvantagens
- Necessita de configurações a mais no tooling
- Curva de aprendizado maior devido a mais detalhes para o funcionamento


# Apollo Client
## Vantagens
- Largamente utilizado no mercado
- Possui sistema de caching/states
- API simplificada e com suporte a hooks
- Muito material sobre online

## Desvantagens
- Extremamente grande
- Atualizações constantes com Breaking Changes
  