# Flutter Basic UI Design

**1. ListView**  
A ListView is very similar to a Column widget. A ListView can also be oriented horizontally (like a Row). The primary difference is that ListView adds scrollable behaviour to its child widgets.

Creating two separate files this time.  
<ins>ListView.dart</ins>

```
import 'package:flutter/material.dart';

class ListViewWidget extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
        return ListView(
        children: [
            createContainer("Canada", Colors.amber),
            createContainer("USA", Colors.blue),
            createContainer("Mexico", Colors.green),
            createContainer("Japan", Colors.brown),
            createContainer("India", Colors.grey),
            createContainer("Russia", Colors.green),
            createContainer("China", Colors.amber),
            createContainer("England", Colors.blue),
            createContainer("Italy", Colors.green),
        ],
        );
    }

    Widget createContainer(String country, Color color) {
        return Container(
        alignment: Alignment.center,
        height: 100,
        color: color,
        child: Text("$country", style: TextStyle(fontSize: 20)),
        );
    }
}
```
<ins>main.dart</ins>
```
import 'package:flutter/material.dart';
import 'ListView.dart';

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
      appBar: AppBar(title: Text("List View")),
      body: ListViewWidget(),
    );
  }
}
```   
**2. GridView**  
Similar to a ListView, a GridView allows scrolling through a list of widgets. Unlike a ListView, GridView can show multiple rows/columns of widgets.

<ins>GridViewWidget.dart</ins>
```
import 'package:flutter/material.dart';

class GridViewWidget extends StatelessWidget {
	@override
	 Widget build(BuildContext context) {
	   return GridView.count(
	     crossAxisCount: 3,
	     children: [
	       ColorfulBox(Colors.red),
	       ColorfulBox(Colors.blue),
	       ColorfulBox(Colors.orange),
	       ColorfulBox(Colors.black),
	       ColorfulBox(Colors.amber),
	       ColorfulBox(Colors.green),
	       ColorfulBox(Colors.brown),
	       ColorfulBox(Colors.cyan),
	       ColorfulBox(Colors.deepPurple),
	       ColorfulBox(Colors.lime),
	       ColorfulBox(Colors.red),
	       ColorfulBox(Colors.blue),
	       ColorfulBox(Colors.orange),
	       ColorfulBox(Colors.black),
	       ColorfulBox(Colors.amber),
	       ColorfulBox(Colors.green),
	       ColorfulBox(Colors.brown),
	       ColorfulBox(Colors.cyan),
	     ],
	    );
  }
}

class ColorfulBox extends StatelessWidget {
  ColorfulBox(this.color) : super();
  final Color color;

  @override
  Widget build(BuildContext context) {
    return Container(
      height: 100,
      width: 100,
      color: color,
    );
  }
}

```
<ins>main.dart</ins>

```
import 'package:flutter/material.dart';
import 'GridViewWidget.dart';

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
          title: Text("Grid View"),
        ),
        body: GridViewWidget());
  }
}
```
**3. Tab Bars**  
Tab screens can be made using the following components:
* A tab controller (DefaultTabController): 
  * Handles the interaction (selecting tabs or swiping)
  * A widget that wraps your Scaffold widget
* A tab bar (TabBar)
  * Displays the options
  * Normally, attached to the bottom of the app bar
* A tab view (TabBarView)
  * Displays the widget for the currently selected view
  * Normally, the body component of the scaffold

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
    return DefaultTabController(
        length: 2,
        child: Scaffold(
          appBar: AppBar(
            title: Text("Grid View"),
            bottom: TabBar(
              tabs: [
                Tab(
                  text: "List View",
                ),
                Tab(text: "Grid View")
              ],
            ),
          ),
          body: TabBarView(
            children: [Text("List View"), Text("Grid View")],
          ),
        ));
  }
}

```