# Dialogs, Pickers and Navigation in Flutter

**1. Dialogs**  
Flutter supports several kinds of dialogs:
* Alert dialogs
* Simple dialogs
* About dialogs
* Custom dialogs


It is always recommended to keep your code clean and tidy by putting them in appropriate files, however, for this lecture, all the code is placed in a single `main.dart` file.

```
import 'package:flutter/material.dart';

	void main() {
	  runApp(MyApp());
	}

	class MyApp extends StatelessWidget {
	  // This widget is the root of your application.
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
	  @override
	  Widget build(BuildContext context) {
	    return Scaffold(
        	appBar: AppBar(
	          title: Text("Dialogs Demo"),
	        ),
	        body: Center(child: ContentArea()));
	  }
	}

	class ContentArea extends StatefulWidget {
	  @override
	  _ContentAreaState createState() => _ContentAreaState();
	}

	class _ContentAreaState extends State<ContentArea> {
	  String myChoice = '';

	  @override
	  Widget build(BuildContext context) {
	    return Column(
	      mainAxisAlignment: MainAxisAlignment.center,
	      children: [
	        ElevatedButton(
	            onPressed: () {
	              _showAlertDialog(context);
	            },
        	    child: Text("Alert Dialog")),
	        Text("You selected $myChoice"),
	      ],
	    );
	  }

	  _showAlertDialog(BuildContext context) {
	    return showDialog(
	        context: context,
	        builder: (BuildContext context) {
	          return AlertDialog(
	            title: Text("Alert Dialog"),
	            content: Text("Do you want a receipt?"),
	            actions: [
	              TextButton(
	                  onPressed: () {	
	                    return Navigator.pop(context, "Yes");
	                  },
	                  child: Text("Yes")),
	              TextButton(
	                  onPressed: () {
	                    return Navigator.pop(context, "No");
	                  },
	                  child: Text("No")),
	            ],
	          );
	        }).then((value) {
	      myChoice = value;
	      setState(() {});
	    });
	  }
	}

```   
**2. Pickers**  
Pickers are like dialogs, but specifically for choosing certain common data types:
* Dates
* Times
* Files
* Images

This program will calculate the age of the person based on the date of birth selected from the Date Picker.
```
	import 'package:flutter/material.dart';

	void main() {
	  runApp(MyApp());
	}

	class MyApp extends StatelessWidget {
	  // This widget is the root of your application.
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
	  @override
	  Widget build(BuildContext context) {
	    return Scaffold(
	        appBar: AppBar(
	          title: Text("Age Calculator"),
	          centerTitle: true,
	        ),
	        body: Center(child: ContentArea()));
	  }
	}

	class ContentArea extends StatefulWidget {
	  @override
	  _ContentAreaState createState() => _ContentAreaState();
	}
	
	class _ContentAreaState extends State<ContentArea> {
	  String selectedDate = '';
	  @override
	  Widget build(BuildContext context) {
	    return Column(
	      mainAxisAlignment: MainAxisAlignment.center,
	      children: [
	        ElevatedButton(
	            onPressed: () {
	              _showDateTimePicker(context);
	            },
	            child: Text("Select Your Birthday")),
	        SizedBox(
	          height: 10,
	        ),
	        Text("You are $selectedDate years old"),
	      ],
	    );
	  }

	  _showDateTimePicker(BuildContext context) {
	    final DateTime initialDate = DateTime.now();
	    final DateTime firstDate = DateTime(2010);
	    final DateTime lastDate = DateTime(2030);
	    return showDatePicker(
	      context: context,
	      initialDate: initialDate,
	      firstDate: firstDate,
	      lastDate: lastDate,
	    ).then((value) {
	      setState(() {
	        var age = DateTime.now().difference(value!);
	        selectedDate = (age.inDays / 365).round().toString();
	      });
	    });
	  }
	}

```
**3. Navigation**  
Flutter has two ways to perform navigation:
* Unnamed routes
* Named routes

```
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.green,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  const MyHomePage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: Text("Dialogs"),
        ),
        body: Center(child: ContentArea()));
  }
}

class ContentArea extends StatefulWidget {
  const ContentArea({Key? key}) : super(key: key);

  @override
  _ContentAreaState createState() => _ContentAreaState();
}

class _ContentAreaState extends State<ContentArea> {
  String myChoice = "Hello World";
  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Text("$myChoice"),
        ElevatedButton(
          onPressed: () {
            Navigator.push(
                context,
                MaterialPageRoute(
                    builder: (context) => SecondScreen(name: "Razi")));
          },
          child: Text("Show Dialog"),
        )
      ],
    );
  }
}

class SecondScreen extends StatefulWidget {
  final String? name;
  const SecondScreen({Key? key, this.name}) : super(key: key);

  @override
  _SecondScreenState createState() => _SecondScreenState();
}

class _SecondScreenState extends State<SecondScreen> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: Text("Second Screen"),
        ),
        body: Center(
          child: Column(
            children: [
              Text("${widget.name}"),
              ElevatedButton(
                  onPressed: () {}, child: Text("Back to Main Screen"))
            ],
          ),
        ));
  }
}

```