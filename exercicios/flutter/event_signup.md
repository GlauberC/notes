## main.dart

```dart
import 'package:event_signup/pages/home.page.dart';
import "package:flutter/material.dart";

void main() {
  runApp(MaterialApp(
      title: "Event Signup",
      home: HomePage(),
      theme: ThemeData(
          primaryColor: Colors.white,
          inputDecorationTheme: InputDecorationTheme(
              enabledBorder: UnderlineInputBorder(
                  borderSide: BorderSide(color: Colors.cyan[900]))))));
}

```

## lib/pages/home.page.dart

```dart
import 'package:flutter/material.dart';

import 'user.page.dart';

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  List _users = [];

  void _addUser() {
    Map<String, String> newUser = Map();
    newUser["name"] = nameController.text;
    newUser["email"] = emailController.text;
    setState(() {
      _users.add(newUser);
    });
    clearInput();
  }

  final nameController = TextEditingController();
  final emailController = TextEditingController();

  void clearInput() {
    nameController.clear();
    emailController.clear();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        backgroundColor: Colors.cyan[700],
        appBar: AppBar(
          title: Text(
            "Cadastro eventos",
            style: TextStyle(color: Colors.white),
          ),
          backgroundColor: Colors.cyan[900],
        ),
        body: Padding(
          padding: EdgeInsets.all(10),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: <Widget>[
              textInputField("Nome Completo", nameController, true),
              Divider(
                color: Colors.transparent,
                height: 10,
              ),
              textInputField("Email", emailController, false),
              Divider(
                height: 10,
                color: Colors.transparent,
              ),
              RaisedButton(
                  onPressed: _addUser,
                  color: Colors.cyan[900],
                  shape: RoundedRectangleBorder(
                      borderRadius: new BorderRadius.circular(18.0),
                      side: BorderSide(color: Colors.cyan[900])),
                  child: Row(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: <Widget>[
                      Text(
                        "Cadastrar",
                        style: TextStyle(color: Colors.white),
                      ),
                      Padding(
                          padding: EdgeInsets.only(left: 10),
                          child: Icon(
                            Icons.person,
                            color: Colors.white,
                          )),
                    ],
                  )),
              Expanded(
                  child: ListView.separated(
                padding: EdgeInsets.all(10),
                itemCount: _users.length,
                itemBuilder: (context, index) {
                  return userItem(context, index);
                },
                separatorBuilder: (context, index) => Divider(
                  color: Colors.transparent,
                ),
              ))
            ],
          ),
        ));
  }

  Widget textInputField(
      String label, TextEditingController controller, bool isText) {
    return TextField(
      keyboardType: isText ? TextInputType.text : TextInputType.emailAddress,
      controller: controller,
      style: TextStyle(color: Colors.white, fontSize: 20),
      cursorColor: Colors.white,
      enableSuggestions: true,
      decoration: InputDecoration(
          border: UnderlineInputBorder(borderSide: BorderSide()),
          labelText: label,
          labelStyle: TextStyle(color: Colors.grey[100], fontSize: 16)),
    );
  }

  Widget userItem(context, index) {
    return ClipRRect(
      key: Key(_users[index]["email"]),
      borderRadius: BorderRadius.all(Radius.circular(5)),
      child: Container(
          color: Colors.white,
          padding: EdgeInsets.all(5),
          child: Row(
            children: <Widget>[
              Expanded(
                child: Column(
                  crossAxisAlignment: CrossAxisAlignment.stretch,
                  children: <Widget>[
                    Text(_users[index]["name"]),
                    Text(_users[index]["email"]),
                  ],
                ),
              ),
              IconButton(
                onPressed: () {
                  Navigator.push(
                      context,
                      MaterialPageRoute(
                          builder: (context) => UserPage(_users[index])));
                },
                color: Colors.cyan[900],
                splashColor: Colors.white,
                icon: Icon(
                  Icons.account_box,
                  size: 35,
                  color: Colors.cyan[900],
                ),
              )
            ],
          )),
    );
  }
}

```

## lib/pages/user.page.dart

```dart
import "package:flutter/material.dart";

class UserPage extends StatelessWidget {
  final Map _user;

  UserPage(this._user);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          _user["name"],
          style: TextStyle(color: Colors.white),
        ),
        backgroundColor: Colors.cyan[900],
      ),
    );
  }
}

```
