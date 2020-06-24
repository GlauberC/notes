## Conteúdos

- Watch changes
- Ocultar o g.dart
- Modelo cliente
- Função textField
- View
- Controller

```
flutter pub build_runner watch
```

## ~/~/.vscode-root/User/settings.json

```json
  "files.exclude": {
    "**/*.g.dart": true
  },
```

## lib/models/client.dart

```dart
import 'package:mobx/mobx.dart';
part 'client.g.dart';

class Client = _ClientBase with _$Client;

abstract class _ClientBase with Store {
  @observable
  String name;

  @action
  changeName(String value) => name = value;

  @observable
  String email;

  @action
  changeEmail(String value) => email = value;

  @observable
  String cpf;

  @action
  changeCpf(String value) => cpf = value;
}

```

## lib/home.dart

```dart
import 'package:curso_mobx/controller.dart';
import 'package:flutter/material.dart';
import 'package:flutter_mobx/flutter_mobx.dart';

class HomePage extends StatelessWidget {
  final controller = Controller();

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
    return Scaffold(
        appBar: AppBar(
          title: Text("Formulário"),
        ),
        body: SingleChildScrollView(
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
                ))));
  }
}

```

## lib/controller.dart

```dart
import 'package:curso_mobx/models/client.dart';
import 'package:mobx/mobx.dart';
part 'controller.g.dart';

class Controller = _ControllerBase with _$Controller;

abstract class _ControllerBase with Store {
  Client client = Client();

  @computed
  bool get isValid {
    return validateName() == null && validateEmail() == null;
  }

  String validateName() {
    if (client.name == null || client.name.isEmpty) {
      return "este campo é obrigatório";
    } else if (client.name.length < 3) {
      return "seu nome precisa ter mais de 3 caracteres";
    }

    return null;
  }

  String validateEmail() {
    if (client.email == null || client.email.isEmpty) {
      return "este campo é obrigatório";
    } else if (!client.email.contains('@')) {
      return "Esse não é um email válido";
    }

    return null;
  }
}

```
