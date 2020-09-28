## Conteúdos

- Separando widgets em arquivos
- InputDecoration.collapsed
- Temas

## lib/main.dart

```dart
import 'package:chat_online/pages/home.page.dart';
import "package:flutter/material.dart";

void main() async {
  runApp(MaterialApp(
    title: "Chat Online",
    debugShowCheckedModeBanner: false,
    home: HomePage(),
    theme: ThemeData(
        primarySwatch: Colors.blue,
        iconTheme: IconThemeData(color: Colors.blue)),
  ));
}

```

## lib/pages/home.page.dart

```dart
import 'package:chat_online/widgets/sendbar.widget.dart';
import 'package:flutter/material.dart';

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.white,
      appBar: AppBar(
        elevation: 0,
        title: Text("Olá, Glauber Carvalho"),
        centerTitle: true,
      ),
      body: Padding(
        padding: EdgeInsets.all(8),
        child: Column(
          children: <Widget>[
            Expanded(
              child: Container(),
            ),
            CustomSendBar()
          ],
        ),
      ),
    );
  }
}

```

## lib/widgets/sendbar.widget.dart

```dart
import "package:flutter/material.dart";

class CustomSendBar extends StatefulWidget {
  @override
  _CustomSendBarState createState() => _CustomSendBarState();
}

class _CustomSendBarState extends State<CustomSendBar> {
  bool _isTyping = false;

  @override
  Widget build(BuildContext context) {
    return Container(
      child: Row(
        children: <Widget>[
          IconButton(
            icon: Icon(Icons.camera_alt),
            onPressed: () {},
          ),
          Expanded(
            child: TextField(
              onChanged: (text) {
                setState(() {
                  _isTyping = text.isNotEmpty;
                });
              },
              onSubmitted: (text) {},
              decoration: InputDecoration.collapsed(
                  hintText: "Enviar uma mensagem",
                  hintStyle: TextStyle(color: Colors.grey[400]),
                  filled: true,
                  fillColor: Colors.white),
            ),
          ),
          IconButton(
              icon: Icon(
                Icons.send,
              ),
              onPressed: _isTyping
                  ? () {
                      print('aloo');
                    }
                  : null),
        ],
      ),
    );
  }
}

```
