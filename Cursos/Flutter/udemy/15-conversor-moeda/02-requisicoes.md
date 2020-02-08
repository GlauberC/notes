## Conteúdos
- http
- get
- json encoded
- async await


## main.dart
```dart
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

const request = "https://api.hgbrasil.com/finance?key=d6dfaa48";

void main() async {
  http.Response response = await http.get(request);
  print(json.decode(response.body));

  print(response.body);
  runApp(MaterialApp(
    title: "Conversor Moeda",
    home: Container(),
  ));
}
```