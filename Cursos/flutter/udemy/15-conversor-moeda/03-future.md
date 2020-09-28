## Conteúdos
- future
- futurebuilder

## main.dart
```dart
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

const request = "https://api.hgbrasil.com/finance?key=d6dfaa48";

void main() async {
  runApp(MaterialApp(
    title: "Conversor Moeda",
    home: HomePage(),
  ));
}

Future<Map> getData() async {
  http.Response response = await http.get(request);
  return json.decode(response.body);
}

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
        backgroundColor: Colors.grey[900],
        appBar: AppBar(
          title: Text("Conversor de moedas"),
          backgroundColor: Colors.yellow[700],
        ),
        body: FutureBuilder<Map>(
            future: getData(),
            builder: (context, snapshot) {
              switch (snapshot.connectionState) {
                case ConnectionState.none:
                case ConnectionState.waiting:
                  return Center(
                      child: CircularProgressIndicator(
                          backgroundColor: Colors.yellow[700],
                          valueColor: new AlwaysStoppedAnimation<Color>(
                              Colors.grey[900])));
                default:
                  if (snapshot.hasError) {
                    return Center(child: Text("Erro"));
                  } else {
                    return Container(child: Text("Carregou"));
                  }
              }
            }));
  }
}

```