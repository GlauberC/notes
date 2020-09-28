## Conteudos
- Importar classe
- ListView
- Staleful

```
Para importar rapidamente CTRL + .
```
## lib/main.dart
```dart
import 'package:flutter/material.dart';
import 'Models/Item.dart';

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

class HomePage extends StatefulWidget {
  var items = new List<Item>();

  // Construtor
  HomePage(){
    items = [];
    items.add(Item(title: 'Item 1', done: false));
    items.add(Item(title: 'Item 2', done: true));
    items.add(Item(title: 'Item 3', done: false));
  }


  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  @override
  Widget build(BuildContext context) {
    // Scaffold - Representa uma página
    return Scaffold(
      // status bar
      appBar: AppBar(
        title: Text('Todo App'),
      ), 
      body: ListView.builder(
        itemCount: widget.items.length,
        itemBuilder: (ctxt, index){
          return Text(widget.items[index].title);
        },
      ),
    );
  }
}

```