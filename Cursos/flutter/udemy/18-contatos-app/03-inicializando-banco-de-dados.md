## Conteúdos
- Db


## lib/helpers/contact.helper.dart
```dart 
import "package:agenda_contatos/models/contact.model.dart";
import 'package:sqflite/sqflite.dart';
import "package:path/path.dart";

final String contactTable = "contactTable";

// Essas coisas estranhas são feitas para que essa classe só passa ter uma instancia
class ContactHelper {
  static final ContactHelper _instance = ContactHelper.internal();

  factory ContactHelper() => _instance;

  ContactHelper.internal();

  // Database
  Database _db;

  Future<Database> get db async {
    if (_db != null) {
      return _db;
    } else {
      _db = await initDb();
      return _db;
    }
  }

  Future<Database> initDb() async {
    final databasesPath = await getDatabasesPath();
    final path = join(databasesPath, "contacts.db");

    return await openDatabase(path, version: 1,
        onCreate: (Database db, int newerVersion) async {
      await db.execute(
          "CREATE TABLE $contactTable($idColumn INTEGER PRIMARY KEY, "
          "$nameColumn TEXT, $emailColumn TEXT, $phoneColumn TEXT, $imgColumn TEXT)");
    });
  }
}

```