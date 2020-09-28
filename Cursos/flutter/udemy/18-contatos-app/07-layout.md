## lib/pages/home.page.dart
```dart
import 'package:agenda_contatos/models/contact.model.dart';
import 'package:flutter/material.dart';
import 'package:agenda_contatos/helpers/contact.helper.dart';

// import "package:agenda_contatos/backup/contact_helper.dart";

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  ContactHelper _contactHelper = ContactHelper();

  List<Contact> contacts = [];

  @override
  void initState() {
    super.initState();
    _contactHelper.getAllContacts().then((list) {
      print(list);
      setState(() {
        contacts = list;
      });
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.red,
        title: Text("Contatos"),
        centerTitle: true,
        actions: <Widget>[
          IconButton(
            onPressed: () {},
            padding: EdgeInsets.only(
              right: 10,
            ),
            icon: Icon(
              Icons.more_horiz,
              color: Colors.white,
            ),
          )
        ],
      ),
      backgroundColor: Colors.white,
      floatingActionButton: FloatingActionButton(
        onPressed: () {},
        backgroundColor: Colors.red,
        child: Icon(Icons.add),
      ),
      body: ListView.builder(
        padding: EdgeInsets.all(10),
        itemCount: contacts.length,
        itemBuilder: (context, index) {},
      ),
    );
  }
}

```