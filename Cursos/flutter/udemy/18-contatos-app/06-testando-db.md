## lib/main.dart
```dart
import 'package:agenda_contatos/pages/home.page.dart';
import "package:flutter/material.dart";

void main() {
  runApp(MaterialApp(
    title: "Contatos App",
    home: HomePage(),
  ));
}

```

## lib/pages/home.page.dart
```dart
import 'package:agenda_contatos/models/contact.model.dart';
import 'package:flutter/material.dart';
import 'package:agenda_contatos/helpers/contact.helper.dart';


class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  ContactHelper _contactHelper = ContactHelper();

  @override
  void initState() {
    super.initState();

    // Contact c = Contact();
    // c.name = "Teste Testado";
    // c.email = "Teste@email.com";
    // c.phone = "84123456789";
    // c.img = "imgtest";

    // _contactHelper.saveContact(c);

    // _contactHelper.getAllContacts().then((list) {
    //   print(list);
    // });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.red,
        title: Text("Contatos"),
        actions: <Widget>[
          IconButton(
            padding: EdgeInsets.only(right: 10, top: 5),
            icon: Icon(
              Icons.more_horiz,
              color: Colors.white,
            ),
          )
        ],
      ),
      floatingActionButton: FloatingActionButton(
        backgroundColor: Colors.red,
        child: Icon(Icons.add),
      ),
    );
  }
}

```