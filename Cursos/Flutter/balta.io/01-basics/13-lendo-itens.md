## Conteúdos
- Métodos assincronos
- Shared preferences


## lib/main.dart
```dart
import 'dart:convert';
import 'package:flutter/material.dart';
import 'Models/Item.dart';
import 'package:shared_preferences/shared_preferences.dart';

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
    // items.add(Item(title: 'Banana', done: false));
    // items.add(Item(title: 'Maçã', done: true));
    // items.add(Item(title: 'Uva', done: false));
  }


  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  var newTaskCtrl = TextEditingController();

  void add(){
    if(newTaskCtrl.text.isEmpty) return;
    setState((){
      widget.items.add(Item(
        title: newTaskCtrl.text, done: false,
      ));

      newTaskCtrl.clear();
    });
  }
  void remove(int index){
    setState((){
      widget.items.removeAt(index);
    });
  }
  Future load() async {
    var prefs = await SharedPreferences.getInstance();
    var data = prefs.getString('data');

    if(data != null){
      Iterable decoded = jsonDecode(data);
      List<Item> result = decoded.map((x) => Item.fromJson(x)).toList();
      setState(() {
        widget.items = result;
      });
    }
  }
  
  _HomePageState(){
    load();
  }

  @override
  Widget build(BuildContext context) {
    // Scaffold - Representa uma página
    return Scaffold(
      // status bar
      appBar: AppBar(
        title: TextFormField(
          controller: newTaskCtrl,
          keyboardType: TextInputType.text,
          style: TextStyle(
            color: Colors.white,
            fontSize: 16,
          ),
          decoration: InputDecoration(
            labelText: "Nova Tarefa",
            labelStyle: TextStyle(
              color: Colors.white
              )
          ),
        ),
      ), 
      body: ListView.builder(
        itemCount: widget.items.length,
        itemBuilder: (ctxt, index){
          final item = widget.items[index];
          return Dismissible(
            child: CheckboxListTile(
            title: Text(item.title),
            value: item.done,
            onChanged: (value){
              setState(() {
                item.done = value;
              });
            }),
            key: Key(item.title),
            background: Container(
              color: Colors.red.withOpacity(0.7),
            ),
            onDismissed: (direction){
              remove(index);
            },
          );
        },
      ),      
      floatingActionButton: FloatingActionButton(
        onPressed: add,
        child: Icon(Icons.add),
      ),
    );
  }
}

```