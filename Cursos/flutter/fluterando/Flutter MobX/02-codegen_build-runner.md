## Conteúdos

- Instalar dev dependences
- usar os decorators para simplificar o código
- Executar o build runner

## pubspec.yaml

```
dev_dependencies:
  flutter_test:
    sdk: flutter
  mobx_codegen:
  build_runner:

```

## lib/controller.dart

```dart
import 'package:mobx/mobx.dart';
part 'controller.g.dart';

class Controller = ControllerBase with _$Controller;

abstract class ControllerBase with Store {
  @observable
  int counter = 0;

  @action
  increment() {
    counter++;
  }
}

```

```
flutter pub run build_runner build
```
