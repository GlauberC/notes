## Listas
```dart
void main(){
  List<String> frutas = ["Maçã", "Uva", "Kiwi"];
  
  print(frutas);
  print(frutas.length);
  
  frutas.add('Banana');
  print(frutas);
  
  frutas.removeAt(2);
  print(frutas);
  
  print(frutas.indexOf("Uva"));
  frutas.removeWhere((fruta) => fruta.startsWith("B"));
  print(frutas);
  
  frutas.insert(1, "Mamão");
  print(frutas);
  
  for (String fruta in frutas){
    print(fruta);
  }
  
}
```
## Mapas
```dart
void main(){
  Map<int, String> ddds = Map();
  ddds[84] = "RN";
  ddds[85] = "CE";
  ddds[83] = "PB";
  
  print(ddds);
  print(ddds.keys);
  print(ddds.values);
  
  print(ddds[84]);

}
```
