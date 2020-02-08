## Conteúdos

- construtor de widgets

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
  final realController = TextEditingController();
  final dolarController = TextEditingController();
  final euroController = TextEditingController();

  double dolar;
  double euro;

  void _realChanged(String text) {
    print(text);
  }

  void _dolarChanged(String text) {
    print(text);
  }

  void _euroChanged(String text) {
    print(text);
  }

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
                              buildTextField("Reais:", "R\$", realController,
                                  _realChanged),
                              Divider(),
                              buildTextField("Dollares:", "US\$",
                                  dolarController, _dolarChanged),
                              Divider(),
                              buildTextField(
                                  "Euros:", "€", euroController, _euroChanged),
                            ]));
                  }
              }
            }));
  }
}

Widget buildTextField(String label, String prefix,
    TextEditingController controller, Function changedFunc) {
  return TextField(
    controller: controller,
    style: TextStyle(color: Colors.yellow[700]),
    onChanged: changedFunc,
    keyboardType: TextInputType.number,
    decoration: InputDecoration(
        labelText: label,
        labelStyle:
            TextStyle(color: Colors.yellow[700], fontWeight: FontWeight.bold),
        border: OutlineInputBorder(),
        prefix: Text(
          "$prefix ",
          style: TextStyle(color: Colors.white),
        )),
  );
}

```
