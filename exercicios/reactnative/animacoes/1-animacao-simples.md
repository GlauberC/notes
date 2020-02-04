# Efeito Fade

- src/pages/Home/index.js
```js
import React, {useState, useEffect} from 'react';
import {View, Text, Animated} from 'react-native';

import {Container, Ball} from './styles';

export default function Home() {
  const [aniValue] = useState(new Animated.Value(0));

  useEffect(() => {
    Animated.timing(aniValue, {
      toValue: 1,
      duration: 1000,
    }).start();
  }, [aniValue]);

  return (
    <Container>
      <Ball style={{opacity: aniValue}} />
    </Container>
  );
}

```
- src/pages/Home/styles.js
```js
import styled from 'styled-components/native';
import {Animated} from 'react-native';

export const Container = styled.View`
  flex: 1;
`;
export const Ball = styled(Animated.View)`
  width: 50px;
  height: 50px;
  background: #f44;
  border-radius: 25px;
`;

```

# Até o fim

```js
import React, {useState, useEffect} from 'react';
import {View, Text, Animated, Dimensions} from 'react-native';

import {Container, Ball} from './styles';

export default function Home() {
  const [aniValue] = useState(new Animated.Value(0));
  const {height, width} = Dimensions.get('window');

  useEffect(() => {
    Animated.timing(aniValue, {
      toValue: height - 75,
      duration: 2000,
    }).start();
  }, [aniValue, height]);

  return (
    <Container>
      <Ball style={{top: aniValue}} />
    </Container>
  );
}

```
# Sequencia e loop

- src/pages/Home/index.js
```js
import React, {useState, useEffect} from 'react';
import {View, Text, Animated, Dimensions} from 'react-native';

import {Container, Ball} from './styles';

export default function Home() {
  const [aniValue] = useState(new Animated.Value(0));
  const {height, width} = Dimensions.get('window');

  useEffect(() => {
    Animated.loop(
      Animated.sequence([
        Animated.timing(aniValue, {
          toValue: height - 75,
          duration: 2000,
        }),
        Animated.timing(aniValue, {
          toValue: 0,
          duration: 2000,
        }),
      ]),
      {
        interations: 4,
      },
    ).start();
  }, [aniValue, height]);

  return (
    <Container>
      <Ball style={{top: aniValue}} />
    </Container>
  );
}

```