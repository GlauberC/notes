## Conteúdos

- Editando controller
- Executar o build runner
- Editando home
- Utilizar computed property para separar a regra de negócio da page

## lib/controller.dart

```dart
import 'package:mobx/mobx.dart';
part 'controller.g.dart';

class Controller = ControllerBase with _$Controller;

abstract class ControllerBase with Store {
  @observable
  String name = '';

  @observable
  String surName = '';

  @computed
  String get fullName => "$name $surName".

  @action
  changeName(String newName) {
    name = newName;
  }

  @action
  changeSurName(String newSurName) {
    surName = newSurName;
  }
}

```

```
flutter pub run build_runner build
```

## lib/home.dart

```dart
import 'package:curso_mobx/controller.dart';
import 'package:flutter/material.dart';
import 'package:flutter_mobx/flutter_mobx.dart';

class HomePage extends StatelessWidget {
  final controller = Controller();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: Text("MobX"),
        ),
        body: Padding(
            padding: EdgeInsets.all(20),
            child: Column(
              children: <Widget>[
                TextField(
                    decoration: InputDecoration(labelText: 'Nome'),
                    onChanged: controller.changeName),
                SizedBox(height: 20),
                TextField(
                    decoration: InputDecoration(labelText: 'Sobrenome'),
                    onChanged: controller.changeSurName),
                SizedBox(height: 20),
                Observer(
                  builder: (_) => Text(
                    controller.fullName,
                    style: TextStyle(fontSize: 18),
                  ),
                )
              ],
            )));
  }
}


```
