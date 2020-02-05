## Conteudos
- CheckboxListTile
  
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
    items.add(Item(title: 'Banana', done: false));
    items.add(Item(title: 'Maçã', done: true));
    items.add(Item(title: 'Uva', done: false));
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
          final item = widget.items[index];
          return CheckboxListTile(
            title: Text(item.title),
            key: Key(item.title),
            value: item.done,
            onChanged: (value){
              print(value);
            },
          );
        },
      ),
    );
  }
}

```