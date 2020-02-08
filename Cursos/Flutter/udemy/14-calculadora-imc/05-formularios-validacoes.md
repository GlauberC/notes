## Conteúdos
- GlobalKey
- Form
- TextFormField
- validator

## main.dart
```dart
import "package:flutter/material.dart";

void main() {
  runApp(MaterialApp(title: "Calculadora IMC", home: HomePage()));
}

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  TextEditingController weightController = TextEditingController();
  TextEditingController heightController = TextEditingController();

  GlobalKey<FormState> _formKey = GlobalKey<FormState>();

  String _infoText = "Informe seus dados!";

  void _resetField() {
    weightController.clear();
    heightController.clear();
    setState(() {
      _infoText = "Informe seus dados!";
      _formKey = GlobalKey<FormState>();
    });
  }

  void _calculate() {
    setState(() {
      double weight = double.parse(weightController.text);
      double height = double.parse(heightController.text) / 100;
      double imc = weight / (height * height);
      if (imc < 18.6) {
        _infoText = "Abaixo do peso (IMC=${imc.toStringAsPrecision(3)})";
      } else if (imc <= 24.9) {
        _infoText = "Peso ideal (IMC=${imc.toStringAsPrecision(3)})";
      } else if (imc <= 29.9) {
        _infoText =
            "Levemente Acima do Peso (IMC=${imc.toStringAsPrecision(3)})";
      } else if (imc <= 34.9) {
        _infoText = "Obesidade Grau I (IMC=${imc.toStringAsPrecision(3)})";
      } else if (imc <= 39.9) {
        _infoText = "Obesidade Grau II (IMC=${imc.toStringAsPrecision(3)})";
      } else {
        _infoText = "Obesidade Grau III (IMC=${imc.toStringAsPrecision(3)})";
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: Text("Calculadora de IMC"),
          centerTitle: true,
          backgroundColor: Colors.green,
          actions: <Widget>[
            IconButton(
              icon: Icon(Icons.refresh),
              onPressed: _resetField,
            )
          ],
        ),
        backgroundColor: Colors.grey[100],
        body: SingleChildScrollView(
            padding: EdgeInsets.fromLTRB(10.0, 0.0, 10.0, 0.0),
            child: Form(
              key: _formKey,
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.stretch,
                children: <Widget>[
                  Icon(
                    Icons.person_outline,
                    size: 120.0,
                    color: Colors.green,
                  ),
                  TextFormField(
                      keyboardType: TextInputType.number,
                      controller: weightController,
                      decoration: InputDecoration(
                          labelText: "Peso (kg)",
                          labelStyle: TextStyle(color: Colors.green)),
                      textAlign: TextAlign.center,
                      style: TextStyle(color: Colors.green, fontSize: 25.0),
                      validator: (value) =>
                          value.isEmpty ? "Insira seu peso" : null),
                  TextFormField(
                      keyboardType: TextInputType.number,
                      controller: heightController,
                      decoration: InputDecoration(
                          labelText: "Altura (cm)",
                          labelStyle: TextStyle(color: Colors.green)),
                      textAlign: TextAlign.center,
                      style: TextStyle(color: Colors.green, fontSize: 25.0),
                      validator: (value) =>
                          value.isEmpty ? "Insira sua altura" : null),
                  Padding(
                      padding: EdgeInsets.only(top: 10, bottom: 10),
                      child: Container(
                        height: 50.0,
                        child: RaisedButton(
                          onPressed: () {
                            if (_formKey.currentState.validate()) {
                              _calculate();
                            }
                          },
                          child: Text(
                            "Calcular",
                            style: TextStyle(
                                fontSize: 25.0, color: Colors.grey[50]),
                          ),
                          color: Colors.green,
                        ),
                      )),
                  Text(
                    _infoText,
                    textAlign: TextAlign.center,
                    style: TextStyle(color: Colors.green, fontSize: 25.0),
                  )
                ],
              ),
            )));
  }
}

```