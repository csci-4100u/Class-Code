# Flutter and HTTP

Http can be used for dealing with Http requests in flutter Add `http:` in `pubspec.yaml`.

Create a function that can handle http requests
```
Future<List<User>> getData() async {
	var url = Uri.http("jsonplaceholder.typicode.com", "/users");
	var response = await get(url);

	var data = jsonDecode(response.body);
	List<User> users = [];
	for (var item in data) {
	    users
	      .add(User(item["id"], item["name"], item["username"], item["email"]));
    }	    
	return users;
}
```
The above function should be part of the MyHomePage class
```
class MyHomePage extends StatelessWidget {
	@override
	Widget build(BuildContext context) {
		return Scaffold(
	      appBar: AppBar(title: Text("Http Request Demo")),
	      body: FutureBuilder(
	        future: getData(),
	        builder: (BuildContext context, AsyncSnapshot snapshot) {
	          if (!snapshot.hasData) {
	            return Center(child: CircularProgressIndicator());
	          }

	          return ListView.builder(
	              itemCount: snapshot.data.length,
	              itemBuilder: (BuildContext context, int index) {
	                return Container(
	                  child: ListTile(
	                    title: Text(snapshot.data[index].name),
	                    subtitle: Text(snapshot.data[index].email),
	                    leading: Text(snapshot.data[index].id.toString()),
	                    trailing: Text(snapshot.data[index].userName),
	                  ),
	                );
	              });
	        },
	      ),
	    );
	  }

	Future<List<User>> getData() async {
	    var url = Uri.http("jsonplaceholder.typicode.com", "/users");
	    var response = await get(url);
	
	    var data = jsonDecode(response.body);
	    List<User> users = [];
	    for (var item in data) {
	      users
	          .add(User(item["id"], item["name"], item["username"], item["email"]));
	    }
	    return users;
	}
}
```
Dont forget to complete the code by putting below code on top of the above code.
```
import 'package:flutter/material.dart';
import 'package:http/http.dart';
import 'dart:convert';

import 'user.dart';

void main() {
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
```
user.dart

```
class User {
	int id;
	String name;
	String username;
	String email;

	User(this.id, this.name, this.username, this.email);

	@override
	String toString(){
		return "User($id, $name, $username, $email)";
	}
}
```
