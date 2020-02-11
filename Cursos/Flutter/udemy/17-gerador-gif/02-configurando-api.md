## main.dart
```dart
import "package:flutter/material.dart";
import "package:buscador_gifs/pages/home.page.dart";

void main() {
  runApp(MaterialApp(title: "Buscador_gif", home: HomePage()));
}

```
## pages/home.page.dart
```dart
import 'dart:convert';

import "package:flutter/material.dart";
import "package:http/http.dart" as http;

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  String _search;
  int _offset = 0;

  Future<Map> _getGifs() async {
    http.Response response;

    if (_search == null)
      response = await http.get(
          "https://api.giphy.com/v1/gifs/trending?api_key=eF02d7Yg06vkf5hP4BWJwpRLtvL9byBc&limit=20&rating=G");
    else
      response = await http.get(
          "https://api.giphy.com/v1/gifs/search?api_key=eF02d7Yg06vkf5hP4BWJwpRLtvL9byBc&q=$_search&limit=20&offset=$_offset&rating=G&lang=pt");

    return json.decode(response.body);
  }

  @override
  void initState() {
    super.initState();
    _getGifs().then((map) {
      print(map);
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(),
    );
  }
}

```