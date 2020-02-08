## Conteúdos

- Border
- OutlineInputBorder
- Divider,
- theme OutlineInputBorder

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
      theme: ThemeData(
          primaryColor: Colors.white,
          inputDecorationTheme: InputDecorationTheme(
              enabledBorder: OutlineInputBorder(
                  borderSide: BorderSide(color: Colors.yellow[700]))))));
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
  double dolar;
  double euro;

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
                    dolar =
                        snapshot.data["results"]["currencies"]["USD"]["buy"];
                    euro = snapshot.data["results"]["currencies"]["EUR"]["buy"];
                    return SingleChildScrollView(
                        padding: EdgeInsets.all(10.0),
                        child: Column(
                            crossAxisAlignment: CrossAxisAlignment.stretch,
                            children: <Widget>[
                              Icon(Icons.monetization_on,
                                  size: 100.0, color: Colors.yellow[700]),
                              Divider(),
                              TextField(
                                style: TextStyle(color: Colors.yellow[700]),
                                decoration: InputDecoration(
                                    labelText: "Reais",
                                    labelStyle: TextStyle(
                                        color: Colors.yellow[700],
                                        fontWeight: FontWeight.bold),
                                    border: OutlineInputBorder(),
                                    prefix: Text(
                                      "R\$ ",
                                      style: TextStyle(color: Colors.white),
                                    )),
                              ),
                              Divider(),
                              TextField(
                                style: TextStyle(color: Colors.yellow[700]),
                                decoration: InputDecoration(
                                    labelText: "Dolares",
                                    labelStyle: TextStyle(
                                        color: Colors.yellow[700],
                                        fontWeight: FontWeight.bold),
                                    border: OutlineInputBorder(),
                                    prefix: Text(
                                      "US\$ ",
                                      style: TextStyle(color: Colors.white),
                                    )),
                              ),
                              Divider(),
                              TextField(
                                style: TextStyle(color: Colors.yellow[700]),
                                decoration: InputDecoration(
                                    labelText: "Euros",
                                    labelStyle: TextStyle(
                                        color: Colors.yellow[700],
                                        fontWeight: FontWeight.bold),
                                    border: OutlineInputBorder(),
                                    prefix: Text(
                                      "€ ",
                                      style: TextStyle(color: Colors.white),
                                    )),
                              ),
                            ]));
                  }
              }
            }));
  }
}

```
