## Conteúdos
- card

## lib/pages/home.page.dart
```dart
import 'dart:io';

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
      print(list.length);
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
        itemBuilder: (context, index) {
          return _contactCard(contacts[index]);
        },
      ),
    );
  }

  Widget _contactCard(Contact contact) {
    return GestureDetector(
        child: Card(
      child: Padding(
          padding: EdgeInsets.all(10),
          child: Row(
            children: <Widget>[
              Container(
                height: 80,
                width: 80,
                decoration: BoxDecoration(
                    shape: BoxShape.circle,
                    image: DecorationImage(
                        image: contact.img == null
                            ? NetworkImage(
                                "https://www.w3schools.com/howto/img_avatar.png")
                            : FileImage(File(contact.img)))),
              ),
              Expanded(
                  child: Padding(
                padding: EdgeInsets.only(left: 10),
                child: Column(
                  crossAxisAlignment: CrossAxisAlignment.stretch,
                  children: <Widget>[
                    Text(
                      contact.name,
                      style:
                          TextStyle(fontWeight: FontWeight.bold, fontSize: 20),
                    ),
                    Text(contact.email,
                        style: TextStyle(color: Colors.black45)),
                    Text(contact.phone, style: TextStyle(color: Colors.black45))
                  ],
                ),
              ))
            ],
          )),
    ));
  }
}

```