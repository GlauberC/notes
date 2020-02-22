## Conteúdos

- duas formas

  - Lendo uma vez
  - Lendo e modificando

## lib/main.dart

```dart
import 'package:chat_online/pages/home.page.dart';
import 'package:cloud_firestore/cloud_firestore.dart';
import "package:flutter/material.dart";

void main() async {
  runApp(MaterialApp(
    title: "Chat Online",
    debugShowCheckedModeBanner: false,
    home: HomePage(),
  ));

  // Lendo apenas uma vez
  QuerySnapshot snapshot =
      await Firestore.instance.collection('mensagens').getDocuments();
  snapshot.documents.forEach((d) {
    print(d.data);
    print(d.documentID);
    d.reference.updateData({'read': true});
  });
  DocumentSnapshot docshot = await Firestore.instance
      .collection('mensagens')
      .document('6Vb3P4C3WXGjUW7xLEZ5')
      .get();
  print(docshot.data);

  // Atualização em tempo real
  Firestore.instance.collection('mensagens').snapshots().listen((dados) {
    dados.documents.forEach((d) {
      print(d.data);
    });
  });
}

```
