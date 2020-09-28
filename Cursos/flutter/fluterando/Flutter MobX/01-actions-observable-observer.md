## Conteúdos

- Instalar dependências
- Template básico do app
- Criar controller
  - Observable
  - Actions
- Home
  - Observer

## pubspec.yaml

```
  mobx:
  flutter_mobx:

```

## lib/main.dart

```dart
import 'package:curso_mobx/home.dart';
import 'package:flutter/material.dart';

void main() {
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
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: HomePage(),
    );
  }
}

```

## lib/controller.dart

```dart
import 'package:mobx/mobx.dart';

class Controller {
  var _counter = Observable(0);
  int get counter => _counter.value;
  set counter(int newValue) => _counter.value = newValue;

  Action increment;

  Controller() {
    increment = Action(_increment);

    autorun((_) {
      print(counter);
    });
  }

  _increment() {
    counter++;
  }
}

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
        floatingActionButton: FloatingActionButton(
            onPressed: () {
              controller.increment();
            },
            child: Icon(Icons.add)),
        body: Center(
            child: Observer(
                builder: (_) => Text(
                      '${controller.counter}',
                      style: TextStyle(fontSize: 40),
                    ))));
  }
}

```
