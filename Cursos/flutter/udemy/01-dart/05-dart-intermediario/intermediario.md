## Operador ternario e etc
```dart
void main(){
  // operador ternario
  int idade = 17;
  String maiorIdade = idade >=18 ? "SIM" : "NÃO";
  print(maiorIdade);
  
  String nome;
  nome = nome ?? "Sem nome"; // Se nome não existir, atribua sem nome
  print(nome);
}
```

## Funções com parametos opcionais e função anonima
```dart
void main(){
  void criarBotao(int height, Function onPress, {String color = "preto"}){
    print("botão criado com tamanho $height e cor $color");
    onPress();
  }
  
  void press(){
    print("Botão apertado");
  }
  
  criarBotao(10, press, color:"azul");
  
  // função anonima
  criarBotao(10, (){
    print("Botão parcialmente apertado");
    }
  );
  
  
}
```