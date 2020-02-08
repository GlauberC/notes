## main.dart
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
      title: "SignUp",
      theme: ThemeData(primarySwatch: Colors.deepPurple),
      home: HomePage()));
}

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  TextEditingController nameController = TextEditingController();
  TextEditingController emailController = TextEditingController();
  TextEditingController passwordController = TextEditingController();
  TextEditingController confirmPasswordController = TextEditingController();
  String _SignUpMsg = "";

  GlobalKey<FormState> _formKey = GlobalKey<FormState>();

  validateEmail(email) {
    return RegExp(
            r"^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,253}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,253}[a-zA-Z0-9])?)*$")
        .hasMatch(email);
  }

  handleSignUp() {
    if (_formKey.currentState.validate()) {
      setState(() {
        _SignUpMsg = "Cadastro realizado com sucesso";
      });
    } else {
      setState(() {
        _SignUpMsg = "";
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: Text(
            "Cadastre-se agora",
            style: TextStyle(color: Colors.white),
          ),
        ),
        body: Padding(
            padding: EdgeInsets.all(10),
            child: SingleChildScrollView(
                child: Form(
              key: _formKey,
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.stretch,
                children: <Widget>[
                  TextFormField(
                    keyboardType: TextInputType.text,
                    controller: nameController,
                    validator: (value) {
                      if (value.isEmpty) {
                        return "Campo nome é obrigatório";
                      } else if (value.length < 6) {
                        return "Nome inválido";
                      } else {
                        return null;
                      }
                    },
                    decoration: InputDecoration(
                        errorStyle: TextStyle(color: Colors.red[700]),
                        labelText: "Nome Completo",
                        labelStyle: TextStyle(
                            color: Colors.deepPurple,
                            fontSize: 18,
                            fontWeight: FontWeight.bold)),
                    style: TextStyle(color: Colors.deepPurple, fontSize: 20),
                  ),
                  Divider(),
                  TextFormField(
                    keyboardType: TextInputType.emailAddress,
                    controller: emailController,
                    validator: (value) {
                      if (value.isEmpty) {
                        return "Campo email é obrigatório";
                      } else if (!validateEmail(value)) {
                        return "Email inválido";
                      } else {
                        return null;
                      }
                    },
                    decoration: InputDecoration(
                        errorStyle: TextStyle(color: Colors.red[700]),
                        labelText: "Email",
                        labelStyle: TextStyle(
                            color: Colors.deepPurple,
                            fontSize: 18,
                            fontWeight: FontWeight.bold)),
                    style: TextStyle(color: Colors.deepPurple, fontSize: 20),
                  ),
                  Divider(),
                  TextFormField(
                    keyboardType: TextInputType.text,
                    obscureText: true,
                    controller: passwordController,
                    validator: (value) {
                      if (value.isEmpty)
                        return "Campo senha é obrigatório";
                      else if (value.length < 6) {
                        return "Senha deve conter pelo menos 6 digitos";
                      } else if (confirmPasswordController.text != value) {
                        return "Senhas não batem";
                      } else {
                        return null;
                      }
                    },
                    decoration: InputDecoration(
                        errorStyle: TextStyle(color: Colors.red[700]),
                        labelText: "Senha",
                        labelStyle: TextStyle(
                            color: Colors.deepPurple,
                            fontSize: 18,
                            fontWeight: FontWeight.bold)),
                    style: TextStyle(color: Colors.deepPurple, fontSize: 20),
                  ),
                  Divider(),
                  TextFormField(
                    keyboardType: TextInputType.text,
                    obscureText: true,
                    controller: confirmPasswordController,
                    validator: (value) {
                      if (value.isEmpty) {
                        return "Campo repita a senha é obrigatório";
                      } else if (passwordController.text != value) {
                        return "Senhas não batem";
                      } else {
                        return null;
                      }
                    },
                    decoration: InputDecoration(
                        errorStyle: TextStyle(color: Colors.red[700]),
                        labelText: "Repita a senha",
                        labelStyle: TextStyle(
                            color: Colors.deepPurple,
                            fontSize: 18,
                            fontWeight: FontWeight.bold)),
                    style: TextStyle(color: Colors.deepPurple, fontSize: 20),
                  ),
                  Divider(
                    height: 40,
                  ),
                  Container(
                    height: 40,
                    child: RaisedButton(
                      color: Colors.deepPurple,
                      onPressed: handleSignUp,
                      child: Row(
                        mainAxisAlignment: MainAxisAlignment.center,
                        children: <Widget>[
                          Text(
                            "Cadastrar",
                            style: TextStyle(fontSize: 18, color: Colors.white),
                          ),
                          Padding(
                            padding: EdgeInsets.only(left: 10),
                            child: Icon(
                              Icons.person_add,
                              color: Colors.white,
                              size: 22,
                            ),
                          )
                        ],
                      ),
                    ),
                  ),
                  Divider(),
                  Text(_SignUpMsg,
                      textAlign: TextAlign.center,
                      style: TextStyle(
                        color: Colors.deepPurple,
                        fontSize: 16,
                      ))
                ],
              ),
            ))));
  }
}

```