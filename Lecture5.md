# Flutter Basic UI Design

**1. Defining Classes**  
The runApp() function takes the given Widget and makes it the root of the widget tree. Example below will make MyApp as the root widget.

	import 'package:flutter/material.dart';

	void main() {
	  runApp(MyApp());
	}

	class MyApp extends StatelessWidget {
	  // This widget is the root of your application.
	  @override
	  Widget build(BuildContext context) {
	    return Center(
	      child: Text(
	        "Hello",
	        textDirection: TextDirection.ltr,
	        style: TextStyle(fontSize: 40),
	      ),
	    );
	  }
	}

**2. Container**  
Container can be used as well to add padding and so on.

	void main() {
	  runApp(MyApp());
	}

	class MyApp extends StatelessWidget {
	  // This widget is the root of your application.
	  @override
	  Widget build(BuildContext context) {
	    return Container(
	      child: Text(
	        "Hello",
	        textDirection: TextDirection.ltr,
	        style: TextStyle(fontSize: 40),
	      ),
	      color: Colors.blue,
	      alignment: Alignment.center,
	    );
	  }
	}

**3. Row**  
Widgets can be arranged in a horizontal manner using Row Widget.

	class MyApp extends StatelessWidget {
	  // This widget is the root of your application.
	  @override
	  Widget build(BuildContext context) {
	    return Row(
	      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
	      children: <Widget>[
	        Text(
	          "Hello",
	          textDirection: TextDirection.ltr,
	          style: TextStyle(fontSize: 40),
	        ),
	        Text(
	          "World",
	          textDirection: TextDirection.ltr,
	          style: TextStyle(fontSize: 40),
	        ),
	      ],
	      textDirection: TextDirection.ltr,
	    );
	  }
	}

**4. Material App**  
It helps you design a basic structure of your app that follows Google's Material App design.

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

	class MyHomePage extends StatelessWidget {
	  Widget build(BuildContext context) {
	    return Container(
	      child: Text(
	        "Hello",
	        style: TextStyle(fontSize: 40),
	        textDirection: TextDirection.ltr,
	      ),
	      color: Colors.blue,
	    );
	  }
	}

**5. Scaffold**  
This is normally the top-level widget in your Material design application.

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

	class MyHomePage extends StatelessWidget {
	  Widget build(BuildContext context) {
	    return Scaffold(
	        appBar: AppBar(
	          title: Text("First Flutter App"),
	        ),
	        body: Center(
	          child: Text("Hello World"),
	        ));
	  }
	}