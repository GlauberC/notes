## Como criar um projeto no firebase
- criar app android no firebase
- colocar o nome do app (ANDROIDMANIFEST)
- colocar sha1 key
- baixar google services.json e colocar em android/app

```sh
keytool -list -v -alias androiddebugkey -keystore ~/.android/debug.keystore -storepass android -keypass android
```

## Configurando autenticaçao
- console.developers.google
- Abra seu projeto no top
- Tela de consentimento OAuth
- Editar aplicativo
- copie o seguinte texto nos 3 ultimos campos https://chatonlineflutter-XXXXa.firebaseapp.com
- Esse texto é idicado um pouco a cima dos campos

## Configurando no vscode para android
## android/app/build.gradle
```
defaultConfig {
        ...
        targetSdkVersion 28
        multiDexEnabled true  // ADD ESSA
        versionCode flutterVersionCode.toInteger()
        ...
    }

...

apply plugin: 'com.google.gms.google-services'

```

## android/build.gradle
```
    dependencies {
        ...
        classpath 'com.google.gms:google-services:4.3.2'
    }
```

## pubspec.yaml
```yaml
  cloud_firestore: ^0.13.0+1
  image_picker: ^0.6.2+3
  google_sign_in: ^4.1.1
  firebase_storage: ^3.1.1
  firebase_auth: ^0.15.3
```

## lib/main.dart
```dart
import 'package:chat_online/pages/home.page.dart';
import 'package:cloud_firestore/cloud_firestore.dart';
import "package:flutter/material.dart";

void main() {
  runApp(MaterialApp(
    title: "Chat Online",
    debugShowCheckedModeBanner: false,
    home: HomePage(),
  ));

  // TESTE FIREBASE
  Firestore.instance
      .collection("col")
      .document("doc")
      .setData({"texto": "Glauber"});
}

```

## lib/pages/home.page.dart
```dart
import 'package:flutter/material.dart';

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold();
  }
}


```
