## lib/main.dart

```dart
import 'package:chat_online/pages/home.page.dart';
import 'package:cloud_firestore/cloud_firestore.dart';
import "package:flutter/material.dart";

void main() {
  runApp(MaterialApp(
    title: "Chat Online",
    debugShowCheckedModeBanner: false,
    home: HomePage(),
  ));

  // Firestore.instance
  //     .collection("col")
  //     .document("doc")
  //     .setData({"texto": "Teste"});

  // Firestore.instance.collection("mensagens").document().setData({
  //   'texto': 'Olá',
  //   'from': 'Daniel',
  //   'read': false,
  // });
  Firestore.instance
      .collection("mensagens")
      .document('GGHPpqUPAe70aSBtlUEr')
      .updateData({
    'read': true,
  });
}

```
