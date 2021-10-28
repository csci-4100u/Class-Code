# Flutter and SQLite

SQFlite is used for working with SQLite in Flutter. Add `sqflite:` to your `pubspec.yaml` before using it.

`main.dart`

```
import 'package:flutter/material.dart';
import 'package:flutter_sqflit_2/add_car.dart';
import 'package:flutter_sqflit_2/db_helper.dart';

	void main() {
	  runApp(const MyApp());
	}

	class MyApp extends StatelessWidget {
	  const MyApp({Key? key}) : super(key: key);

	  @override
	  Widget build(BuildContext context) {
	    return MaterialApp(
	      title: 'Flutter Demo',
	      theme: ThemeData(
	        primarySwatch: Colors.blue,
      		),
	      home: const MyHomePage(),
	      routes: {
	        '/addCar': (context) => AddCarWidget(),
	      },
	    );
	  }
	}

	class MyHomePage extends StatefulWidget {
	  const MyHomePage({Key? key}) : super(key: key);

	  @override
	  _MyHomePageState createState() => _MyHomePageState();
	}

	class _MyHomePageState extends State<MyHomePage> {
	  List<String> cars = [];

	  @override
	  void initState() {
	    // TODO: implement initState
	    super.initState();
	    getAllData();
	  }

	  @override
	  Widget build(BuildContext context) {
	    return Scaffold(
	      appBar: AppBar(title: Text("Cars")),
	      body: ListView.builder(
        	  itemCount: cars.length,
        	  itemBuilder: (BuildContext context, int index) {
	            return Container(
	              padding: const EdgeInsets.all(10.0),
	              child: ListTile(
	                title: Text(
	                  cars[index],
	                  style: const TextStyle(fontSize: 18),
	                ),
	                onTap: () async {
	                  print(cars[index]);
	                  int result =
	                      await DBHelper.dbHelper.deleteByName(cars[index]);
	                  setState(() {
	                    getAllData();
	                  });
	                },
	              ),
	            );
	          }),
	      floatingActionButton: FloatingActionButton(
	        onPressed: () async {
	          var result = await Navigator.pushNamed(context, '/addCar');
	          if (result == true) {
	            setState(() {
	              getAllData();
	            });
	          }
	        },
	        child: const Icon(Icons.add),
	      ),
	    );
	  }
	
	  getAllData() async {
	    List<Map<String, dynamic>> record = await DBHelper.dbHelper.getData();
	    setState(() {
	      cars.clear();
	      record.forEach((element) {
	        cars.add(element["name"]);
	      });
	    });
	  }
	}
```   
`add_car.dart`

```
import 'package:flutter/material.dart';
import 'db_helper.dart';

	class AddCarWidget extends StatelessWidget {
	  AddCarWidget({Key? key}) : super(key: key);
	  TextEditingController _controller = TextEditingController();
	
	  @override
	  Widget build(BuildContext context) {
	    return Scaffold(
	      appBar: AppBar(
	        title: const Text("Add a car"),
	        automaticallyImplyLeading: false,
	      ),
	      body: Column(
	        children: [
	          TextField(
	            controller: _controller,
	            decoration: const InputDecoration(labelText: "Enter a car"),
	          ),
	          ElevatedButton(
	              onPressed: () async {
	                int result = await DBHelper.dbHelper
	                    .insertData({"name": _controller.text});
	                print(result);
	                Navigator.pop(context, true);
	              },
	              child: const Text("Add Car"))
	        ],
	      ),
	    );
	  }
	}
```

`db_helper.dart`

```
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

	class DBHelper {
	  DBHelper._privateConstructor();

	  static DBHelper dbHelper = DBHelper._privateConstructor();

	  late Database _database;

	  Future<Database> get database async {
	    _database = await _createDatabase();

	    return _database;
	  }

	  Future<Database> _createDatabase() async {
	    Database database =
	        await openDatabase(join(await getDatabasesPath(), 'mydb.db'),
	            onCreate: (Database db, int version) {
	      db.execute("CREATE TABLE Cars(id INTEGER PRIMARY KEY, name TEXT)");
	    }, version: 1);
	    return database;
	  }
	
	  Future<int> insertData(Map<String, dynamic> row) async {
	    Database db = await database;
	    return db.insert("Cars", row);
	  }
	
	  Future<List<Map<String, dynamic>>> getData() async {
	    Database db = await database;
	    return await db.query("Cars");
	  }
	
	  Future<List<Map<String, dynamic>>> getDatabyName(String name) async {
	    Database db = await database;
	    return await db.query("Cars", where: "id=?", whereArgs: [name]);
	  }
	
	  Future<int> deleteByName(String name) async {
	    Database db = await database;
	    return await db.delete("Cars", where: "name=?", whereArgs: [name]);
	  }
	}
	
```