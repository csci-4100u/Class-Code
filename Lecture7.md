# Stateful Widgetes and Forms in Flutter

**1. Stateful Widget**  
If a widget can change—when a user interacts with it, for example—it’s stateful. A stateful widget is dynamic: for example, it can change its appearance in response to events triggered by user interactions or when it receives data. Some examples are:
* Checkbox
* Radio
* Slider
* Form
* TextField

It is always recommended to keep your code clean and tidy by putting them in appropriate files, however, for this lecture, all the code is placed in a single `main.dart` file.

```
import 'package:flutter/material.dart';

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

	class MyHomePage extends StatelessWidget {
	  @override
	  Widget build(BuildContext context) {
	    return Scaffold(
	      appBar: AppBar(title: Text("Stateful Widgets")),
	      body: Center(child: ContentArea()),
	    );
	  }
	}

	class ContentArea extends StatefulWidget {
	  @override
	  _ContentAreaState createState() => _ContentAreaState();
	}

	class _ContentAreaState extends State<ContentArea> {
	  Color _color = Colors.blue;
	  @override
	  Widget build(BuildContext context) {
	    return ElevatedButton(
	      onPressed: () {
	        setState(() {
	          _color = Colors.amber;
	        });
	      },
	      child: Text("Click Me"),
	      style: ElevatedButton.styleFrom(primary: _color),
	    );
	  }
	}
```   
**2. Changing State of One Widget from Another**  
In Fluter, state of one widget can be changed from another widget using `setState()` method that would force Flutter to call the `build()` method.

```
class ContentArea extends StatefulWidget {
	  @override
	  _ContentAreaState createState() => _ContentAreaState();
	}

	class _ContentAreaState extends State<ContentArea> {
	  int _counter = 0;
	  @override
	  Widget build(BuildContext context) {
	    return Column(
	      mainAxisAlignment: MainAxisAlignment.center,
	      children: [
	        Text(
	          '$_counter',
	          style: TextStyle(fontSize: 20),
	        ),
	        ElevatedButton(
	            onPressed: () {
	              setState(() {
	                _counter++;
	              });
	            },
	            child: Text("Click Me"))
	      ],
	    );
	  }
	}
```
**3. Forms**  
Forms are used for validating the fields. Special TextFields called TextFormFields are used in forms.


```
import 'package:flutter/material.dart';

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

	class MyHomePage extends StatelessWidget {
	  @override
	  Widget build(BuildContext context) {
	    return Scaffold(
	        appBar: AppBar(
	          title: Text("Login"),
	        ),
	        body: FormWidget());
	  }
	}

	class FormWidget extends StatefulWidget {
	  const FormWidget({Key? key}) : super(key: key);
	
 	 @override
	  _FormWidgetState createState() => _FormWidgetState();
	}

	class _FormWidgetState extends State<FormWidget> {
	  final GlobalKey<FormState> _formKey = GlobalKey<FormState>();
	  String? _email = '';
	  String? _password = '';
	  @override
	  Widget build(BuildContext context) {
	    return Container(
	        padding: EdgeInsets.all(20.0),
	        child: Form(
	            key: _formKey,
	            child: Column(
	                mainAxisAlignment: MainAxisAlignment.start,
	                crossAxisAlignment: CrossAxisAlignment.start,
	                children: [
	                  TextFormField(
	                    decoration: InputDecoration(labelText: "Email"),
	                    validator: (value) {
	                      if (value == null || value.isEmpty) {
	                        return 'This field cant be null';
	                      }
	                      return null;
	                    },
	                    onSaved: (value) {
	                      _email = value;
	                    },
	                  ),
	                  TextFormField(
	                    obscureText: true,
	                    decoration: InputDecoration(labelText: "Password"),
	                    validator: (value) {
	                      if (value == null || value.isEmpty) {
	                        return 'This field cant be null';
	                      }
	                      return null;
	                    },
	                    onSaved: (value) {
	                      _password = value;
	                    },
	                  ),
	                  ElevatedButton.icon(
	                      onPressed: () {
	                        if (_formKey.currentState!.validate()) {
	                          ScaffoldMessenger.of(context).showSnackBar(SnackBar(
	                            content: Text("Logged In successfully"),
	                          ));
	                        }
	                      },
	                      icon: Icon(Icons.login),
	                      label: Text("Login"))
	                ])));
	  }
	}


```