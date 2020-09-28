## Conteúdos

- Separando body
- Configurando os providers
- Usando os Providers

## pubspec.yaml

```yaml
provider:
```

## lib/home.dart

```dart
import 'package:curso_mobx/body.dart';
import 'package:curso_mobx/controller.dart';
import 'package:flutter/material.dart';
import 'package:flutter_mobx/flutter_mobx.dart';
import 'package:provider/provider.dart';

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final controller = Provider.of<Controller>(context);
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
import 'package:provider/provider.dart';

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
    final controller = Provider.of<Controller>(context);
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

## lib/main.dart

```dart
import 'package:curso_mobx/home.dart';
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

import 'controller.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MultiProvider(
      providers: [
        Provider<Controller>(
          create: (_) => Controller(),
        )
      ],
      child: MaterialApp(
        title: 'Flutter Demo',
        theme: ThemeData(
          primarySwatch: Colors.blue,
          buttonColor: Colors.blue,
          visualDensity: VisualDensity.adaptivePlatformDensity,
        ),
        home: HomePage(),
      ),
    );
  }
}

```
