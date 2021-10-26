# State Management

**1. Without BLoC**  
States can be managed using setState() method. A traditional way:

`main.dart`

```
import 'MyHomePage.dart';

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
```   
`MyHomePage.dart`

```
import 'package:flutter/material.dart';

	class MyHomePage extends StatefulWidget {
	  @override
	  _MyHomePageState createState() => _MyHomePageState();
	}

	class _MyHomePageState extends State<MyHomePage> {
	  var _counter = 0;

	  @override
	  Widget build(BuildContext context) {
	    return Scaffold(
	        appBar: AppBar(
	          title: Text('BLoC Demo'),
	        ),
        	body: Center(
	          child: Text(
	            "$_counter",
        	    style: TextStyle(fontSize: 24),
	          ),
	        ),
        	floatingActionButton: Row(
	          mainAxisAlignment: MainAxisAlignment.end,
	          children: [
	            FloatingActionButton(
	              child: Icon(Icons.add),
	              onPressed: () => _incrementCounter(),
	            ),
	            SizedBox(
	              width: 8,
	            ),
	            FloatingActionButton(
	              child: Icon(Icons.remove),
	              onPressed: () => _decrementCounter(),
	            ),
	          ],
	        ));
	  }

	  _incrementCounter() {
	    setState(() {
	      _counter++;
	    });
	  }

	  _decrementCounter() {
	    setState(() {
	      _counter--;
	    });
	  }
	}
```

**2. Using BLoC Approach**  
The above approach is not a good practice. BLoC is much better approach. Provider framework is used for this purpose in this exercise. Add `provider:` to `pubspec.yaml`

`main.dart`

```
void main() {
	  runApp(MultiProvider(
	      providers: [ChangeNotifierProvider(create: (_) => ProviderHelper())],
	      child: MyApp()));
	}


	class MyApp extends StatelessWidget {
	
	  @override
	  Widget build(BuildContext context) {
	    return MaterialApp(
	      title: 'Flutter Demo',
	      theme: ThemeData(
	        primarySwatch: Colors.blue,
	      ),
	      home: MyHomePageProvider(),
	    );
	  }
	}
```
`MyHomePageProvider.dart`

```
import 'package:bloc_increment_decrement/providerHelper.dart';
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

	class MyHomePageProvider extends StatefulWidget {
	  @override
	  _MyHomePageProviderState createState() => _MyHomePageProviderState();
	}

	class _MyHomePageProviderState extends State<MyHomePageProvider> {
	  @override
	  Widget build(BuildContext context) {
	    return Scaffold(
	        appBar: AppBar(
	          title: Text('BLoc Demo'),
	        ),
	        body: Center(
	          child: Text(
	            "${context.watch<ProviderHelper>().counter}",
	            style: TextStyle(fontSize: 24),
	          ),
	        ),
	        floatingActionButton: Row(
	          mainAxisAlignment: MainAxisAlignment.end,
	          children: [
	            FloatingActionButton(
	              child: Icon(Icons.add),
	              onPressed: () =>
        	          context.read<ProviderHelper>().incrementCounter(),
	            ),
	            SizedBox(
	              width: 8,
	            ),
        	    FloatingActionButton(
	              child: Icon(Icons.remove),
	              onPressed: () =>
	                  context.read<ProviderHelper>().decrementCounter(),
	            ),
	          ],
	        ));
	  }
	}

```
`provider_helper.dart`
```
import 'package:flutter/foundation.dart';

	class ProviderHelper with ChangeNotifier {
	  var counter = 0;
	
	  incrementCounter() {
	    counter++;
	    print(counter);
	    notifyListeners();
	  }

	  decrementCounter() {
	    counter--;
	    print(counter);
	    notifyListeners();
	  }
	}
```

**3. Working with ListView using BLoC**  
A more practical approach is to update a ListView using BLoC approach.

`provider_helper.dart`

```
class Fruit {
	  String name;

	  Fruit(this.name);

	  @override
	  String toString() {
	    return "$name";
	  }
	}

class ProviderHelper with ChangeNotifier {
	  List<Fruit> _fruits = [];

	  List<Fruit> get fruits => _fruits;

	  addFruits(Fruit fruit) {
	    _fruits.add(fruit);
	    notifyListeners();
	  }
	}

```
`main.dart`

```
import 'package:bloc_listview/add_fruits.dart';
import 'package:bloc_listview/provider_helper.dart';
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

	void main() {
	  runApp(MultiProvider(
	    providers: [ChangeNotifierProvider(create: (_) => ProviderHelper())],
	    child: MyApp(),
	  ));
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
	      routes: {
	        '/add_fruits': (context) => AddFruitsWidget(),
	      },
	    );
	  }
	}

	class MyHomePage extends StatelessWidget {
	  @override
	  Widget build(BuildContext context) {
	    return Scaffold(
	      appBar: AppBar(title: Text("Fruits")),
	      body: ScaffoldBodyContent(),
	      floatingActionButton: FloatingActionButton(
	        child: Icon(Icons.add),
	        onPressed: () {
	          Navigator.pushNamed(context, '/add_fruits');
	        },
	      ),
	    );
	  }
	}

	class ScaffoldBodyContent extends StatelessWidget {
	  @override
	  Widget build(BuildContext context) {
	    ProviderHelper providerHelper = context.watch<ProviderHelper>();
	    print(providerHelper.fruits);
	    return ListView.builder(
	        itemCount: providerHelper.fruits.length,
	        itemBuilder: (BuildContext context, int index) {
	          return Container(
	            padding: EdgeInsets.all(10.0),
	            child: Text(
	              "${providerHelper.fruits[index]}",
	              style: TextStyle(fontSize: 16.0),
	            ),
	          );
	        });
	  }
	}
```
`add_fruits.dart`

```
import 'package:bloc_listview/provider_helper.dart';
	import 'package:flutter/material.dart';
	import 'package:provider/provider.dart';

	class AddFruitsWidget extends StatefulWidget {
	  const AddFruitsWidget({Key? key}) : super(key: key);

	  @override
	  _AddFruitsWidgetState createState() => _AddFruitsWidgetState();
	}

	class _AddFruitsWidgetState extends State<AddFruitsWidget> {
	  TextEditingController _controller = TextEditingController();
	  @override
	  Widget build(BuildContext context) {
	    ProviderHelper providerHelper = Provider.of<ProviderHelper>(context);
	    return Scaffold(
	      appBar: AppBar(
	        title: Text("Add Fruit"),
	      ),
	      body: Center(
        	  child: Column(
	        children: [
        	  TextField(
	            controller: _controller,
	            decoration: InputDecoration(labelText: "Enter a Fruit"),
	          ),
	          ElevatedButton(
        	      onPressed: () {
	                Fruit fruit = new Fruit("${_controller.text}");
	                providerHelper.addFruits(fruit);
	                Navigator.pop(context);
	              },
	              child: Text("Add Fruit"))
	        ],
	      )),
	    );
	  }
	}


```

