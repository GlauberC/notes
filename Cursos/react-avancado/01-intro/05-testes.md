# Por que testes ?
- Código complexo não é simples de se debuggar só com olho
- Testar é uma forma robusta de validar software
  - Funciona como eu espero?
  - Funciona como o usuário espera?
  - Se eu atualizar esse trecho, o código quebra ?
- Testes funcionam como uma primeira camada documentação

# Que tipos de testes existem? 
## Testes unitários
  - Testam isoladamente pequenas unidades de código
  - O código está se comportando como o desenvolvedor espera ?
  - 
## Testes Funcionais
  - Chega se as unidades funcionam também entre si
  - Testes podem conter múltiplas classes métodos, etc
  - O programa funciona de acordo com o que o usuário espera?

# Exemplo, um buscador de filmes
## Features
- Expande quando em foco
- Envia um request para um banco com a palavra digitada
- Recebe dados e renderiza na tela a lista 
- Destaca dentro dos itens a string digitada
- Quando não possui nenhum item, mostra um mensagem
  
## Testes unitários
- Isolamos só o componente de busca (criando mock para o serviço)
- Testamos cada um dos comportamentos de forma separada
  - Se o campo recebe focus, ele expande? (adição de classe, por exemplo)
  - Ao ter uma string no campo, o método de fetch da API é chamado?
  - A string do campo é passada corretamente para a API e os dados retornados são condizentes ?
  - Dado um conjunto de dados recebido, a lista é renderizada?
  - Se não tiver dados, uma mensagem é preenchida ?

## Testes funcionais
- Aqui não há mais isolamento entre os mé todos e nós, realizamos o fluxo completo
  - Simula usuário clicando
  - Simula usuário digitando e apagando
  - Simula usuário clicando num item de pesquisa
- Analisa todo o fluxo para ver se o comportamento funciona 