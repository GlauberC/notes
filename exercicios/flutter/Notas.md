## main.dart

```dart
import "package:flutter/material.dart";

void main() {
  runApp(MaterialApp(
    title: "NotasApp",
    home: HomePage(),
    theme: ThemeData(
        primaryColor: Colors.blue,
        hintColor: Colors.grey[500],
        inputDecorationTheme: InputDecorationTheme(
            enabledBorder: OutlineInputBorder(
                borderSide: BorderSide(
          color: Colors.blue,
        )))),
  ));
}

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  TextEditingController nota1Controller = TextEditingController();
  TextEditingController nota2Controller = TextEditingController();
  TextEditingController nota3Controller = TextEditingController();
  TextEditingController recuController = TextEditingController();
  double media;
  double notaFinal;

  Widget recuperacao() {
    if (media != null && media < 7)
      return Column(
        children: <Widget>[
          Divider(),
          Text(
            'Sua media foi ${media.toStringAsPrecision(3)}',
            style: TextStyle(
                color: Colors.blue, fontWeight: FontWeight.bold, fontSize: 18),
          ),
          Divider(),
          inputFieldFactory("Digite a nota da recuperação:", recuController),
        ],
      );
    else {
      return Text("");
    }
  }

  Widget notaFinalFunc() {
    if (notaFinal != null)
      return Column(
        children: <Widget>[
          Divider(),
          Text(
            'Sua media final foi ${notaFinal.toStringAsPrecision(3)}',
            style: TextStyle(
                color: Colors.blue, fontWeight: FontWeight.bold, fontSize: 18),
          ),
        ],
      );
    else {
      return Text("");
    }
  }

  resetBtn() {
    setState(() {
      media = null;
      notaFinal = null;
      recuController.clear();
      nota1Controller.clear();
      nota2Controller.clear();
      nota3Controller.clear();
    });
  }

  Widget message() {
    if (notaFinal != null) {
      if (notaFinal >= 7) {
        return Column(children: <Widget>[
          Divider(),
          Text(
            'Parabéns você foi aprovado',
            style: TextStyle(
                color: Colors.green, fontWeight: FontWeight.bold, fontSize: 18),
          ),
          Divider(),
          RaisedButton(
            color: Colors.blue,
            onPressed: resetBtn,
            child: Icon(Icons.refresh, color: Colors.white),
          )
        ]);
      } else {
        return Column(children: <Widget>[
          Divider(),
          Text(
            'Infelizmente você não passou',
            style: TextStyle(
                color: Colors.red, fontWeight: FontWeight.bold, fontSize: 18),
          ),
          RaisedButton(
            color: Colors.blue,
            onPressed: resetBtn,
            child: Icon(Icons.refresh, color: Colors.white),
          )
        ]);
      }
    }
    return Text("");
  }

  addBtn() {
    double mediaParcial;
    if (media == null) {
      mediaParcial = (double.parse(nota1Controller.text) +
              double.parse(nota2Controller.text) +
              double.parse(nota3Controller.text)) /
          3;
    }
    setState(() {
      if (mediaParcial != null && mediaParcial >= 7) {
        notaFinal = mediaParcial;
      } else if (media != null) {
        notaFinal = (media + double.parse(recuController.text)) / 2;
      } else {
        media = mediaParcial;
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: Text("Cadastro de notas"),
        ),
        body: SingleChildScrollView(
            padding: EdgeInsets.all(10),
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.stretch,
              children: <Widget>[
                inputFieldFactory("Digite a nota 1", nota1Controller),
                Divider(),
                inputFieldFactory("Digite a nota 2", nota2Controller),
                Divider(),
                inputFieldFactory("Digite a nota 3", nota3Controller),
                recuperacao(),
                notaFinalFunc(),
                message(),
              ],
            )),
        floatingActionButton: FloatingActionButton(
          onPressed: addBtn,
          child: Icon(Icons.add),
        ));
  }
}

Widget inputFieldFactory(label, controller) {
  return TextField(
      controller: controller,
      keyboardType: TextInputType.numberWithOptions(decimal: true),
      style: TextStyle(color: Colors.blue, fontSize: 18),
      decoration: InputDecoration(
        labelText: label,
        border: OutlineInputBorder(),
      ));
}

```
