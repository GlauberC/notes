# Problemas do css
- Falta de escopo local (uma lib de terceiros pode colidir com meu código)
- Especificidade e novamente, colisão de estilos
- Código não utilizado (dead code)
- Falta de modularidade
- Dificuldade na manutenção e código quebrando em algum outro lugar

# Pré-processadores
- Less, Sass, Stylus
- Vieram ajudar em algumas coisas, mas continuaram com os problemas clássicos, além de abrir margem para péssimas práticas

# Css-in-Js
- Conjunto de ideias para resolver os complexos problemas do CSS. E existem diferentes bibliotecas que fazem essa prática
- Aphrodite, Emotion, Glamor, Styled Components, Styled JSX

# Vantagens do Styled Components
- Critical CSS automático
- Escopo definido (sem colisão de classes)
- Remoção de CSS não utilizado
- Estilos dinâmicos (props, themes)
- Manutenção simplificada e sem dor
- Vendor prefixing automático