## Stateless widget
- Não guarda estados
- Atalho: **stl**
```dart
class NAME extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      
    );
  }
}
```

## Stateful widget
- guarda estados
- Atalho: **stf**
```dart
class NAME extends StatefulWidget {
  @override
  _NAMEState createState() => _State();
}

class _NAMEState extends State<> {
  @override
  Widget build(BuildContext context) {
    return Container(
      
    );
  }
}
```

