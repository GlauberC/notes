## Conteúdos

- add data in firebase
- pass function between widgets in diferent files

## lib/pages/home.page.dart

```dart
import 'package:chat_online/widgets/sendbar.widget.dart';
import 'package:cloud_firestore/cloud_firestore.dart';
import 'package:flutter/material.dart';

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  void _sendMessage(String text) {
    Firestore.instance
        .collection('messages')
        .add({'text': text, 'from': 'Glauber Carvalho'});
  }

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
            CustomSendBar((text) {
              _sendMessage(text);
            })
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
  CustomSendBar(this.sendMessage);
  Function(String) sendMessage;

  @override
  _CustomSendBarState createState() => _CustomSendBarState();
}

class _CustomSendBarState extends State<CustomSendBar> {
  bool _isTyping = false;

  final _msgController = TextEditingController();

  _send(text) {
    widget.sendMessage(text);
    _msgController.clear();
    setState(() {
      _isTyping = false;
    });
  }

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
              controller: _msgController,
              onChanged: (text) {
                setState(() {
                  _isTyping = text.isNotEmpty;
                });
              },
              onSubmitted: (text) {
                _send(text);
              },
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
                      _send(_msgController.text);
                    }
                  : null),
        ],
      ),
    );
  }
}

```
