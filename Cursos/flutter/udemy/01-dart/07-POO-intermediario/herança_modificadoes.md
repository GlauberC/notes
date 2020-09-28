## Herança
```dart
class Pessoa{
  String nome;
  int idade;
  
  Pessoa(this.nome, this.idade);
  
  fazAniversario(){
    this.idade++;
  }
}

class Aluno extends Pessoa{
  String matricula;
  
  Aluno(String nome, int idade, this.matricula) : super(nome, idade);
}

class Professor extends Pessoa{
  int salario;
  
  Professor(String nome, int idade, this.salario) : super(nome, idade);
}

void main(){
  
  Aluno a1 = new Aluno("João", 19, "20200001234");
  Professor p1 = new Professor("Paulo", 40, 2000);
  
  print(a1.nome);
  print(a1.matricula);
  
  print(p1.nome);
  print(p1.salario);
  
}
```

## polimorfismo
```dart
class Pessoa{
  String nome;
  int idade;
  
  Pessoa(this.nome, this.idade);
  
  fazAniversario(){
    this.idade++;
  }
  dever(){
    print("${this.nome} foi trabalhar");
  }
}

class Aluno extends Pessoa{
  String matricula;
  
  Aluno(String nome, int idade, this.matricula) : super(nome, idade);
  
  @override
  dever(){
    print("${this.nome} foi pra aula");
  }
  
  @override
  String toString(){
    return "Aluno $nome; Matricula: ${this.matricula}";
  }
}

class Professor extends Pessoa{
  int salario;
  
  Professor(String nome, int idade, this.salario) : super(nome, idade);
  
}

void main(){
  
  Aluno a1 = new Aluno("João", 19, "20200001234");
  Professor p1 = new Professor("Paulo", 40, 2000);
  
  print(a1.nome);
  print(a1.matricula);
  a1.dever();
  print(a1);
  
  print(p1.nome);
  print(p1.salario);
  p1.dever();
  
}
```

## Modificador Const, Final, Static
- **const** utilizado quando se conhece o valor inicial (PI é um exemplo), isso vai criar uma referencia na memória de rápido acesso (pois se conhece posição e tamanho em bits desde o inicio)

- **final** é utilizado quando se quer uma constante, porém não se conhece de início o valor. Ele vai criar um efeito semelhante ao const depois de inicializado, porém tem o tempo de alocação de memória quando ele for utilizado.

- **Static** é um atributo ou método da propria classe

## Classe abstrata
- Basta colocar **abstract** antes da classe. Classes abstratas não podem ser instanciadas.