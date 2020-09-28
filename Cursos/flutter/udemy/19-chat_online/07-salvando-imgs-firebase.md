## Conteúdos

- ativando o storage
- salvando file no storage

## firebase StorageRules

```
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read, write: if true;
    }
  }
}

```

## lib/pages/home.page.dart

```dart
import 'dart:io';

import 'package:chat_online/widgets/sendbar.widget.dart';
import 'package:cloud_firestore/cloud_firestore.dart';
import 'package:firebase_storage/firebase_storage.dart';
import 'package:flutter/material.dart';

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  void _sendMessage({String text, File imgFile}) async {
    Map<String, dynamic> data = {};

    if (imgFile == null) {
      data['text'] = text;
    } else {
      // StorageUploadTask task = FirebaseStorage.instance.ref().child('pasta').child(path)
      StorageUploadTask task = FirebaseStorage.instance
          .ref()
          .child(DateTime.now().millisecondsSinceEpoch.toString())
          .putFile(imgFile);
      StorageTaskSnapshot taskSnapshot = await task.onComplete;
      String url = await taskSnapshot.ref.getDownloadURL();
      data['imgUrl'] = url;
    }

    Firestore.instance.collection('messages').add(data);
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
            CustomSendBar(({String text, File imgFile}) {
              _sendMessage(
                text: text,
                imgFile: imgFile,
              );
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
import 'dart:io';

import "package:flutter/material.dart";
import 'package:image_picker/image_picker.dart';

class CustomSendBar extends StatefulWidget {
  CustomSendBar(this.sendMessage);
  final Function({String text, File imgFile}) sendMessage;

  @override
  _CustomSendBarState createState() => _CustomSendBarState();
}

class _CustomSendBarState extends State<CustomSendBar> {
  bool _isTyping = false;

  final _msgController = TextEditingController();

  _send(text) {
    widget.sendMessage(text: text);
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
            onPressed: () async {
              final File imgFile =
                  await ImagePicker.pickImage(source: ImageSource.camera);
              if (imgFile == null) return;
              widget.sendMessage(imgFile: imgFile);
            },
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
