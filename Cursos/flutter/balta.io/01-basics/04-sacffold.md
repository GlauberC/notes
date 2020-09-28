## Conteudos
- Page
- Statusbar
- Center


## lib/main.dart
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
        title: 'Todo App', // titulo da aplicação,
        debugShowCheckedModeBanner: false, //tira o nome debug de cima
        theme: ThemeData(
          primarySwatch: Colors.red,
        ),
        home: HomePage());
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Scaffold - Representa uma página
    return Scaffold(
      // status bar
      appBar: AppBar(
        title: Text('Todo App'),
      ), 
      body: Container(
        child: Center(child: Text("Olá mundo"),
        ),
      ),
    );
  }
}

```