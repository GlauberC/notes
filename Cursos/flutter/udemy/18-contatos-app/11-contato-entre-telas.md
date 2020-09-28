## Conteúdos

- recebendo valores entre telas

## lib/main.dart

```dart

import 'package:agenda_contatos/pages/home.page.dart';
import "package:flutter/material.dart";

void main() {
  runApp(MaterialApp(
    debugShowCheckedModeBanner: false,
    title: "Contatos App",
    // home: HomePage(),
    home: HomePage(),
  ));
}


```

## lib/pages/home.page.dart

```dart
import 'dart:io';

import 'package:agenda_contatos/models/contact.model.dart';
import 'package:agenda_contatos/pages/contact.page.dart';
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

  void _getAllContacts() {
    _contactHelper.getAllContacts().then((list) {
      setState(() {
        contacts = list;
      });
    });
  }

  @override
  void initState() {
    super.initState();
    _getAllContacts();
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
        onPressed: () {
          _showContactPage();
        },
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
        onTap: () {
          _showContactPage(contact: contact);
        },
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
                          style: TextStyle(
                              fontWeight: FontWeight.bold, fontSize: 20),
                        ),
                        Text(contact.email,
                            style: TextStyle(color: Colors.black45)),
                        Text(contact.phone,
                            style: TextStyle(color: Colors.black45))
                      ],
                    ),
                  ))
                ],
              )),
        ));
  }

  _showContactPage({Contact contact}) async {
    final recContact = await Navigator.push(
        context,
        MaterialPageRoute(
            builder: (context) => ContactPage(
                  contact: contact,
                )));
    if (recContact != null) {
      if (contact != null) {
        await _contactHelper.updateContact(recContact);
      } else {
        await _contactHelper.saveContact(recContact);
      }
      _getAllContacts();
    }
  }
}

```

## lib/pages/contact.page.dart

```dart
import 'dart:io';

import "package:flutter/material.dart";
import "package:agenda_contatos/models/contact.model.dart";

class ContactPage extends StatefulWidget {
  final Contact contact;
  ContactPage({this.contact});

  @override
  _ContactPageState createState() => _ContactPageState();
}

class _ContactPageState extends State<ContactPage> {
  Contact _editedContact;

  bool _userEdited = false;

  final _nameController = TextEditingController();
  final _emailController = TextEditingController();
  final _phoneController = TextEditingController();

  @override
  void initState() {
    super.initState();

    if (widget.contact == null) {
      _editedContact = Contact();
    } else {
      _editedContact = Contact.fromMap(widget.contact.toMap());
      _nameController.text = _editedContact.name;
      _emailController.text = _editedContact.email;
      _phoneController.text = _editedContact.phone;
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.red,
        title: Text(_editedContact.name == null || _editedContact.name.isEmpty
            ? "Novo Contato"
            : _editedContact.name),
        centerTitle: true,
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {},
        child: Icon(Icons.save),
        backgroundColor: Colors.red,
      ),
      body: SingleChildScrollView(
          padding: EdgeInsets.all(10),
          child: Column(
            children: <Widget>[
              GestureDetector(
                child: Center(
                  child: Container(
                    height: 160,
                    width: 160,
                    decoration: BoxDecoration(
                        shape: BoxShape.circle,
                        image: DecorationImage(
                            image: _editedContact.img == null
                                ? NetworkImage(
                                    "https://www.w3schools.com/howto/img_avatar.png")
                                : FileImage(File(_editedContact.img)))),
                  ),
                ),
              ),
              TextField(
                keyboardType: TextInputType.text,
                enableSuggestions: true,
                controller: _nameController,
                onChanged: (text) {
                  _userEdited = true;

                  setState(() {
                    _editedContact.name = text;
                  });
                },
                decoration: InputDecoration(labelText: "Nome"),
              ),
              Divider(),
              TextField(
                controller: _emailController,
                enableSuggestions: true,
                keyboardType: TextInputType.emailAddress,
                onChanged: (text) {
                  _userEdited = true;
                  _editedContact.email = text;
                },
                decoration: InputDecoration(labelText: "Email"),
              ),
              Divider(),
              TextField(
                controller: _phoneController,
                keyboardType: TextInputType.phone,
                onChanged: (text) {
                  _userEdited = true;
                  _editedContact.phone = text;
                },
                decoration: InputDecoration(labelText: "Phone"),
              ),
              Divider(),
            ],
          )),
    );
  }
}

```
