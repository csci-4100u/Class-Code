# Flutter and FireStore

Firebase is a back-end for mobile (and web) development.

Below are steps to setup Firebase
1. Sign in with your google id.
2. Create a Firebase project.
3. Project ID should match your application ID of Flutter.
    * Go to Android > app > build.gradle and get the id from application ID.
		- Also change minSDKVersion to 21
	* Copy the following plugin to Andriod > app > build.gradle
		apply plugin: `com.google.gms.google-services`
	* Copy the following dependencies in Android > build.gradle
	        classpath `com.google.gms:google-services:4.3.10`
	* Download `google-services.json` and add to Android > app >

Firebase should now be setup.  

Add following dependencies in Flutter pubspec.yaml and save it.
```
  firebase_core:
  cloud_firestore:
```
Add the following line to avoid sound null safety
```
// @dart=2.9
```
Now setup a Database in Firebase by clicking Firestore Database and creating a collection.

Create Vehicle collection and add some documents with all strings.
```
name : Apple
quantity: 8
```
	
Setup the main method to look like this:

```
void main() async {
    WidgetsFlutterBinding.ensureInitialized();
	await Firebase.initializeApp();
	runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  String _selectedValue = 'All';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(title: Text("Firestore Demo")),
        body: StreamBuilderWidget(
          selection: _selectedValue,
        ),
        bottomNavigationBar: Container(
          padding: EdgeInsets.all(20.0),
          child: DropdownButton(
       	    value: _selectedValue,
            items: <String>["All", "Apple", "Banana", "Orange", "Grape"]
	              .map<DropdownMenuItem<String>>((String value) {
	              return DropdownMenuItem<String>(value: value, child: Text(value));
	            }).toList(),
	            onChanged: (value) {
	              setState(() {
	                _selectedValue = value;
	                print(_selectedValue);
	              });
	            },
	          ),
	        ));
	  }
	}
```
stream_helper.dart

```
// @dart=2.9
import 'package:flutter/material.dart';
import 'package:cloud_firestore/cloud_firestore.dart';
import 'package:firebase_core/firebase_core.dart';

class StreamBuilderWidget extends StatefulWidget {
  String selection = '';
  StreamBuilderWidget({Key key, this.selection}) : super(key: key);

  @override
  _StreamBuilderWidgetState createState() => _StreamBuilderWidgetState();
}

class _StreamBuilderWidgetState extends State<StreamBuilderWidget> {
  final fruits = FirebaseFirestore.instance.collection('fruits');

	@override
	 Widget build(BuildContext context) {
	   return StreamBuilder(
	     stream: getData(),
	     builder: (BuildContext context, AsyncSnapshot<QuerySnapshot> snapshot) {
	       if (!snapshot.hasData) return Text("No Data");
	       return ListView.builder(
	           itemCount: snapshot.data.docs.length,
	           itemBuilder: (BuildContext context, int index) {
	             final docData = snapshot.data.docs[index].data();
	              return ListTile(
	                title: Text(docData["name"].toString()),
	              );
	            });
	      },
	    );
	  }

	  Stream<QuerySnapshot> getData() {
	    if (widget.selection == "All") {
	      return fruits.snapshots();
	    }
	    return fruits.where('name', isEqualTo: widget.selection).snapshots();
	  }
	}
```
	