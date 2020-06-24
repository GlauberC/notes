## Conteúdos

- Configurando get_it
- Usando no código

## lib/main.dart

```dart
import 'package:curso_mobx/home.dart';
import 'package:flutter/material.dart';
import 'package:get_it/get_it.dart';

import 'controller.dart';

void main() {
  GetIt getIt = GetIt.I;
  getIt.registerSingleton<Controller>(Controller());

  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        buttonColor: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: HomePage(),
    );
  }
}

```

## lib/home.dart

```dart
import 'package:curso_mobx/body.dart';
import 'package:curso_mobx/controller.dart';
import 'package:flutter/material.dart';
import 'package:flutter_mobx/flutter_mobx.dart';
import 'package:get_it/get_it.dart';

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final controller = GetIt.I.get<Controller>();
    return Scaffold(
        appBar: AppBar(
            title: Observer(
          builder: (_) => Text(controller.isValid
              ? "Formulário Validado"
              : "Formulário não validado"),
        )),
        body: Body());
  }
}

```

## lib/body.dart

```dart
import 'package:curso_mobx/controller.dart';
import 'package:flutter/material.dart';
import 'package:flutter_mobx/flutter_mobx.dart';
import 'package:get_it/get_it.dart';

class Body extends StatelessWidget {
  _textField({String labelText, onChanged, String Function() errorText}) {
    return TextField(
        onChanged: onChanged,
        decoration: InputDecoration(
            border: OutlineInputBorder(),
            labelText: labelText,
            errorText: errorText == null ? null : errorText()));
  }

  @override
  Widget build(BuildContext context) {
    final controller = GetIt.I.get<Controller>();
    return SingleChildScrollView(
        child: Padding(
            padding: EdgeInsets.all(20),
            child: Column(
              children: <Widget>[
                Observer(
                    builder: (_) => _textField(
                          labelText: "name",
                          onChanged: controller.client.changeName,
                          errorText: controller.validateName,
                        )),
                SizedBox(height: 20),
                Observer(
                    builder: (_) => _textField(
                          labelText: "email",
                          onChanged: controller.client.changeEmail,
                          errorText: controller.validateEmail,
                        )),
                SizedBox(height: 20),
                // Observer(
                //     builder: (_) => _textField(
                //           labelText: "cpf",
                //           onChanged: controller.client.changeCpf,
                //           errorText: controller.validateCpf,
                //         )),
                // Observer(builder: (_)=> ,)
                // Observer(builder: (_)=> ,)
                SizedBox(height: 40),
                Observer(
                    builder: (_) => RaisedButton(
                          onPressed: controller.isValid
                              ? () {
                                  print('oi');
                                }
                              : null,
                          child: Text('Salvar'),
                        ))
              ],
            )));
  }
}

```
