## lib/main.dart

```dart
import "package:flutter/material.dart";
import 'package:flutter/services.dart';
import 'package:wid/pages/home.page.dart';

void main() {
  SystemChrome.setSystemUIOverlayStyle(
      SystemUiOverlayStyle(statusBarColor: Colors.black.withOpacity(0.2)));
  runApp(MaterialApp(
    title: "WID",
    home: HomePage(),
  ));
}

```

## lib/pages/home.page.dart

```dart
import 'dart:async';
import 'dart:math';

import "package:flutter/material.dart";
import 'package:flutter/services.dart';
import 'package:wakelock/wakelock.dart';
import "package:wid/data/word.data.dart";

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  List _allWords = getAllWords();

  List _rightAnswers = [];
  List _wrongAnswers = [];

  int _dreamerTime = 120;
  int _tipsTime = 4;
  bool _isDream = false;
  List _wordSequence = [];
  List _pastWords = [];
  int _keyValue = 0;
  final _random = new Random();

  void _randomWord() {
    String element;
    do {
      element = _allWords[_random.nextInt(_allWords.length)];
    } while (_pastWords.indexOf(element) > -1);
    setState(() {
      _keyValue = _keyValue + 1;
      _wordSequence.add(element);
      _pastWords.add(element);
    });
  }

  void _restart() {
    setState(() {
      _isDream = false;
      _tipsTime = 4;
      _dreamerTime = 120;
      _keyValue = 0;
      _wordSequence.clear();
      _rightAnswers.clear();
      _wrongAnswers.clear();
      _pastWords.clear();
    });
  }

  void _missTip() {
    if (_dreamerTime < 120) {
      _wordSequence.clear();
      _randomWord();
    }
  }

  void _startDream() {
    if (_isDream == false) {
      setState(() {
        _isDream = true;
        Wakelock.enable();
        _tipsTime = 4;
        _startTips();
      });
      _randomWord();
      const oneSec = const Duration(seconds: 1);
      new Timer.periodic(
        oneSec,
        (Timer timer) => setState(
          () {
            if (_dreamerTime < 1) {
              _isDream = false;
              Wakelock.disable();

              timer.cancel();
            } else {
              if (_isDream == true)
                _dreamerTime = _dreamerTime - 1;
              else
                timer.cancel();
            }
          },
        ),
      );
    }
  }

  void _startTips() {
    const oneSec = const Duration(seconds: 1);
    new Timer.periodic(
      oneSec,
      (Timer timer) => setState(
        () {
          if (_tipsTime < 1) {
            SystemSound.play(SystemSoundType.click);
            _tipsTime = 4;
          } else {
            if (_isDream) {
              _tipsTime = _tipsTime - 1;
            } else {
              timer.cancel();
            }
          }
        },
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
            centerTitle: true,
            backgroundColor: Colors.blue[50],
            leading: _isDream == false
                ? IconButton(
                    onPressed: _startDream,
                    icon: Icon(
                      Icons.play_arrow,
                      color: Colors.black,
                    ),
                    iconSize: 42,
                  )
                : null,
            title: Text(
              _dreamerTime.toString(),
              style: TextStyle(
                  fontSize: 48,
                  color: _dreamerTime > 20
                      ? Colors.black
                      : _dreamerTime > 5
                          ? Colors.yellow[800]
                          : Colors.red[600]),
            )),
        backgroundColor: Colors.blue[50],
        body: Column(
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: <Widget>[
            Expanded(
              flex: 1,
              child: ListView.builder(
                itemCount: _wordSequence.length,
                itemBuilder: (context, index) {
                  return Dismissible(
                      key: Key(_keyValue.toString()),
                      direction: DismissDirection.horizontal,
                      background: Container(
                        padding: EdgeInsets.only(left: 10),
                        color: Colors.red[400],
                        child: Align(
                            alignment: Alignment.centerLeft,
                            child: Icon(
                              Icons.check_circle,
                              size: 32,
                              color: Colors.white,
                            )),
                      ),
                      secondaryBackground: Container(
                        padding: EdgeInsets.only(right: 10),
                        color: Colors.blue[400],
                        child: Align(
                            alignment: Alignment.centerRight,
                            child: Icon(
                              Icons.clear,
                              size: 32,
                              color: Colors.white,
                            )),
                      ),
                      onDismissed: (DismissDirection direction) {
                        if (direction == DismissDirection.endToStart) {
                          setState(() {
                            _keyValue = _keyValue + 1;
                            _wrongAnswers.add(_wordSequence.removeLast());
                          });
                        } else {
                          setState(() {
                            _keyValue = _keyValue + 1;
                            _rightAnswers.add({
                              "title": _wordSequence.removeLast(),
                              "ok": false
                            });
                          });
                        }
                        _randomWord();
                      },
                      child: Column(
                        crossAxisAlignment: CrossAxisAlignment.stretch,
                        children: <Widget>[
                          Container(
                            color: Colors.white,
                            padding: EdgeInsets.all(20),
                            child: Text(
                              _wordSequence[index],
                              style: TextStyle(
                                  fontSize: 38, color: Colors.red[900]),
                              textAlign: TextAlign.center,
                            ),
                          )
                        ],
                      ));
                },
              ),
            ),
            Expanded(
                flex: 3,
                child: Row(
                  children: <Widget>[
                    Expanded(
                      child: Container(
                        color: Colors.red[100],
                        child: ListView.builder(
                          itemCount: _rightAnswers.length,
                          itemBuilder: (context, index) {
                            return CheckboxListTile(
                              title: Text(
                                _rightAnswers[index]["title"],
                                style: TextStyle(
                                    color: Colors.black, fontSize: 20),
                              ),
                              value: _rightAnswers[index]["ok"],
                              activeColor: Colors.red[300],
                              onChanged: (checked) {
                                setState(() {
                                  _rightAnswers[index]["ok"] = checked;
                                });
                              },
                            );
                          },
                        ),
                      ),
                    ),
                    Expanded(
                        child: Container(
                      color: Colors.blue[200],
                      child: ListView.builder(
                          itemCount: _wrongAnswers.length,
                          itemBuilder: (context, index) {
                            return ListTile(
                              title: Text(
                                _wrongAnswers[index],
                                style: TextStyle(
                                    color: Colors.black, fontSize: 20),
                              ),
                            );
                          }),
                    ))
                  ],
                )),
            Divider(),
            RaisedButton(
              onPressed: () {},
              padding: EdgeInsets.all(10),
              onLongPress: _restart,
              color: Colors.red[100],
              child: Text(
                "Recomeçar partida",
              ),
            ),
            Divider(),
            RaisedButton(
              onPressed: () {},
              padding: EdgeInsets.all(10.0),
              onLongPress: _missTip,
              color: Colors.blue[100],
              child: Text(
                "Errou dica",
              ),
            ),
            Text(
              "Dicas:",
              textAlign: TextAlign.center,
            ),
            Text(
              _tipsTime.toString(),
              textAlign: TextAlign.center,
              style: TextStyle(
                  color: _tipsTime < 1 ? Colors.red : Colors.black,
                  fontSize: 32),
            )
          ],
        ));
  }
}


```

## lib/data/word.data.dart

```dart
List getAllWords() {
  return [
    'Abacate',
    'Abajur',
    'Abóbora',
    'Academia',
    'Açaí',
    'Açucar',
    'Advogado',
    'Aeroporto',
    'África',
    'Agenda',
    'Água',
    'Águia',
    'Alemanha',
    'Algodão',
    'Alienígena',
    'Ambulância',
    'Aniversário',
    'Anjo',
    'Antártica',
    'Aplauso',
    'Aquário',
    'Ar Condicionado',
    'Aranha',
    'Arco-Íris',
    'Argentina',
    'Arroz',
    'Assassino',
    'Astronauta',
    'Austrália',
    'Avestruz',
    'Avião',
    'Bacon',
    'Balança',
    'Balão',
    'Baleia',
    'Banana',
    'Banco',
    'Banda',
    'Bandeira',
    'Bar',
    'Barata',
    'Barco',
    'Basquete',
    'Bateria',
    'Batom',
    'Bebê',
    'Boia',
    'Bola',
    'Bolha',
    'Bolo',
    'Bolsa',
    'Bomba',
    'Bombeiro',
    'Borboleta',
    'Borracha',
    'Bosque',
    'Bota',
    'Botão',
    'Braço',
    'Brasil',
    'Brigadeiro',
    'Brinco',
    'Bronze',
    'Bruxa',
    'Buraco Negro',
    'Bússola',
    'Buzina',
    'Cabeça',
    'Cabelo',
    'Cachorro',
    'Cachorro-Quente',
    'Cadeira',
    'Caderno',
    'Caixa',
    'Calça',
    'Calçada',
    'Calção',
    'Cama',
    'Camaleão',
    'Câmera',
    'Caminhão',
    'Camisa',
    'Caneta',
    'Canguru',
    'Caramelo ',
    'Carne',
    'Carregador',
    'Carro',
    'Carta',
    'Carta',
    'Carvão',
    'Casaco',
    'Casca',
    'Casino',
    'Castelo',
    'Cavaleiro',
    'Cavalo',
    'Cebola',
    'Cegonha',
    'Celular',
    'Cemitério',
    'Centauro',
    'Cerca',
    'Cerveja',
    'Céu',
    'Chave',
    'Chave de Fenda',
    'Chicote',
    'China',
    'Chocolate',
    'Churrasqueira',
    'Chuteira',
    'Chuva',
    'Chuveiro',
    'Cientista',
    'Cigarro',
    'Cinto',
    'Cobra',
    'Coelho',
    'Cola',
    'Colar',
    'Colchão',
    'Colher',
    'Computador',
    'Constelação',
    'Contrato',
    'Copo',
    'Coqueiro',
    'Coração',
    'Coroa',
    'Corpo',
    'Corrente',
    'Corrida',
    'Coxinha',
    'Cozinheiro',
    'Criança',
    'Cruz',
    'Dado',
    'Dança',
    'Dedo',
    'Dente',
    'Desenho',
    'Dia',
    'Diabo',
    'Diamante',
    'Dinamite',
    'Dinheiro',
    'Dinossauro',
    'Doce de Leite',
    'Doença',
    'Dominó',
    'Dragão',
    'Egito',
    'Elefante',
    'Elevador',
    'Embaixada',
    'Enfermeira',
    'Engenheiro',
    'Engrenagem',
    'Ervilha',
    'Escada',
    'Escola',
    'Escorpião',
    'Esgoto',
    'Espada',
    'Espaguete',
    'Espião',
    'Espinho',
    'Esqueleto',
    'Estação',
    'Estádio',
    'Estados Unidos',
    'Estagiário',
    'Estátua',
    'Estrada',
    'Estrela',
    'Estudante',
    'Fábrica',
    'Faca',
    'Fada',
    'Falcão',
    'Família',
    'Fantasma',
    'Farofa',
    'Farrmácia',
    'Favela',
    'Fechadura',
    'Feijão',
    'Feijoada',
    'Ferro',
    'Filho',
    'Filme',
    'Física',
    'Flauta',
    'Floresta',
    'Fogo',
    'Fogueira',
    'Foguete',
    'Folha',
    'Formiga',
    'Forno',
    'Fotografia',
    'Fralda',
    'França',
    'Frango',
    'Furacão',
    'Furadeira',
    'Futebol',
    'Garfo',
    'Garrafa',
    'Gato',
    'Gelo',
    'Geografia',
    'Gladiador',
    'Gramado',
    'Granola',
    'Gravata',
    'Grécia',
    'Grilo',
    'Guacamole',
    'Guarda-Roupa',
    'Guitarra',
    'Hamburguer',
    'Helicóptero',
    'História',
    'Hóspital',
    'Idoso',
    'Igreja',
    'Ilha',
    'Índio',
    'Inferno',
    'Internet',
    'Interruptor',
    'Irmão',
    'Itália',
    'Jacaré',
    'Janela',
    'Japão',
    'Juíz',
    'Ketchup',
    'Lã',
    'Lábio',
    'Laboratório',
    'Ladrão',
    'Lagoa',
    'Lâmpada',
    'Lápis',
    'Laranja',
    'Leão',
    'Lençol',
    'Licença',
    'Limão',
    'Língua',
    'Linguiça',
    'Liquidificador',
    'Loja',
    'Lua',
    'Lupa',
    'Maçã',
    'Macaco',
    'Mãe',
    'Maionese',
    'Mala',
    'Manga',
    'Manual',
    'Mar',
    'Máscara',
    'Matemática',
    'Médico',
    'Meia',
    'Melancia',
    'Melão',
    'Mergulhador',
    'Mesa',
    'Metal',
    'Meteóro',
    'Metralhadora',
    'Metrô',
    'México',
    'Micro-Ondas',
    'Microfone',
    'Microscópio',
    'Milho',
    'Milionário',
    'Montanha',
    'Motor',
    'Motorista',
    'Museu',
    'Música',
    'Nariz',
    'Natal',
    'Návio',
    'Neve',
    'Ninja',
    'Noite',
    'Nova Iorque',
    'Novela',
    'Oceano',
    'Óleo',
    'Olho',
    'Onda',
    'Ónibus',
    'Orelha',
    'Ossos',
    'Ouro',
    'Ovelha',
    'Pá',
    'Padre',
    'Pai',
    'Palavra',
    'Panda',
    'Panela',
    'Papél',
    'Para-Quedas',
    'Parafuso',
    'Paraíso',
    'Paris',
    'Parque',
    'Páscoa',
    'Passaro',
    'Pastel',
    'Pastor',
    'Pato',
    'Pegada',
    'Peixe',
    'Pena',
    'Perna',
    'Petróleo',
    'Piano',
    'Pilha',
    'Piloto',
    'Pimenta',
    'Pincel',
    'Pirâmide',
    'Pirata',
    'Piscina',
    'Pistola',
    'Pizza',
    'Placa',
    'Planeta',
    'Plástico',
    'Policial',
    'Político',
    'Polvo',
    'Ponte',
    'População',
    'Porco',
    'Porta',
    'Porta-Retrato',
    'Porto',
    'Português',
    'Praça',
    'Praia',
    'Prata',
    'Prato',
    'Professor',
    'Pulmão',
    'Quadrado',
    'Quadro',
    'Queijo',
    'Química',
    'Rádio',
    'Raínha',
    'Raio',
    'Raiz',
    'Rato',
    'Receita',
    'Rede',
    'Refrigerante',
    'Rei',
    'Relógio',
    'Revista',
    'Rinoceronte',
    'Rio',
    'Rio de Janeiro',
    'Robô',
    'Roda',
    'Roleta',
    'Roma',
    'Rosa',
    'Saia',
    'Sal',
    'Salada',
    'Samurai',
    'Sandália',
    'Sanduíche',
    'São Paulo',
    'Sapato',
    'Sapo',
    'Satélite',
    'Semente',
    'Shopping',
    'Sofá',
    'Sol',
    'Soldado',
    'Sorvete',
    'Suco',
    'Super Mercado',
    'Taco',
    'Tanque',
    'Tapete',
    'Tatuagem',
    'Teatro',
    'Teia',
    'Telefone',
    'Telescópio',
    'Televisão',
    'Tempestade',
    'Templo',
    'Tênis',
    'Termômetro',
    'Terno',
    'Terra',
    'Terremoto',
    'Tesoura',
    'Tigre',
    'Tinta',
    'Tocha',
    'Tomada',
    'Tomate',
    'Torpedo',
    'Torre',
    'Touro',
    'Travesseiro',
    'Trem',
    'Triângulo',
    'Tronco',
    'Trovão',
    'Tsunami',
    'Turista',
    'Unicórnio',
    'Universidade',
    'Universo',
    'Urso',
    'Urubu',
    'Uva',
    'Vaca',
    'Vampiro',
    'Vela',
    'Veneno',
    'Ventilador',
    'Vento',
    'Vestido',
    'Video-Game',
    'Vidro',
    'Violão',
    'Vôlei',
    'Vulcão',
    'Xícara',
    'Zoológico',
  ];
}

```
