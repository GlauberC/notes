## Conteudos
- Class
- DartToJson
  -  https://javiercbk.github.io/json_to_dart/

## lib/models/Item.dart
```dart
class Item {
  String title;
  bool done;

  Item({this.title, this.done});

  // Métodos para enviar e receber json
  Item.fromJson(Map<String, dynamic> json) {
    title = json['title'];
    done = json['done'];
  }

  Map<String, dynamic> toJson() {
    final Map<String, dynamic> data = new Map<String, dynamic>();
    data['title'] = this.title;
    data['done'] = this.done;
    return data;
  }
}
```