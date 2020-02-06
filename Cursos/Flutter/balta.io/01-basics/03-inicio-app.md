# Diferenças Android e IOS
```dart
import 'package:flutter/material.dart'; // Design Android
import 'package:flutter/cupertino.dart'; // Design IOS
```

# Inicio do app
## lib/main.dart
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
        title: 'Todo App', // titulo da aplicação,
        theme: ThemeData(
          primarySwatch: Colors.red,
        ),
        home: HomePage());
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container();
  }
}

```