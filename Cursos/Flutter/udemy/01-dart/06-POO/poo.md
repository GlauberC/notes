## Classes e Named constructors
```dart

class Carro{
  String _dono;
  String _cor;
  String _marca;
  
  Carro(this._dono, this._cor, this._marca);
  Carro.fabricado(this._cor, this._marca); //named constructor
  
  String get dono{
    return _dono;
  }
  String get cor{
    return _cor;
  }
  String get marca => _marca;
  
  set dono(String dono){
    _dono = dono;
  }
}


void main(){
  Carro carro1 = new Carro("Glauber", "azul", "Ford");
  print(carro1.dono);
  
  Carro carro2 = new Carro.fabricado("Branco", "Chevrolet");
  print(carro2.marca);
  
  carro2.dono = "Glauber";
  print(carro2.dono);
}
```