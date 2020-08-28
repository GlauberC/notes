# NextJS
- Renderização no servidor (SSR)
- Geração de estáticos (SSG)
- CSS-in-JS (Styled-jsx, Styled Components, Emotions)
- Zero configuration (rotas, hot reloading, code splitting...)
- Completamente extensível (controle completo do babel/webpack, plugins...)
- Otimizado para produção

# Tipos de aplicação
- Static site(HTML/CSS/JS) - GatsbyJS, Hexo, NextJS
- Client Side Rendering (Single Page Application - SPA) - Create React App, NextJS
- Server Side Rendering(SSR) - NextJS

# Static Site Generation
## Vantagens
- Uso quase nulo do servidor
- Pode ser servido numa CDN (melhor cache)
- Melhor performance entre todos
- Flexibilidade para usar qualquer servidor

## Desvantagens
- Tempo de build pode ser muito alto
- Dificuldade para escalar em aplicações grandes
- Dificuldade para realizar atualizações constantes


# Single Page Application
## Vantagens
- Permite páginas ricas em interações sem recarregar 
- Site rápido após o load inicial
- Ótimo para aplicações web
- Possui diversas bibliotecas

## Desvantagens
- Load inicial pode ser muito grande
- Performance imprevisível
- Dificuldades no SEO

# Server Side Rendering
## Vantagens
- Ótimo em SEO
- Meta tags com previews mais adequados
- Melhor performance para o usuário (o conteúdo vai ser visto mais rápido)
- Código compartilhado com o backend em Node
- Menor processamento no lado do usuário 
## Desvantagens
- TTFB(Time to first byte) maior, o servidor vai preparar todo o conteúdo para entregar 
- HTML maior
- Reload completo nas mudanças de rota*

# Quando usar cada um ?
## Static Site Generation
- Site simples sem muita interação do usuário
- Se você é a única pessoa que publica conteúdo
- Se o conteúdo muda pouco
- Se o site é simples, sem tantas páginas
- Quando a performance é extremamente importante
- Exemplos: Landing Page, Blogs, Portfólios

## Single Page Application
- Quando não tem tanta necessidade de indexar informações do Google
- Quando o usuário faz muitas interações na página e não quero refreshes
- Quando as informações vão ser diferentes para cada usuário (autenticação, por exemplo)
- Exemplos: Twitter Web, Facebook Web, Spotify Web

## Server Side Rendering
- Quando tem necessidades de um SPA, mas precisa de um loading mais rápido
- Quando o conteúdo muda frequentemente
- Quando trabalha com um número muito grande de páginas
- Quando precisa de uma boa indexação no Google
- Exemplo: Ecommerce, Sites de Notícias