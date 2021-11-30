# Orientation Detection in Flutter

1. OrientationBuilder can help detect the orientation
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
	        appBar: AppBar(title: Text("Orientation Demo")),
        	body: OrientationBuilder(builder: (context, orientation) {
	          return GridView.count(
	            crossAxisCount: orientation == Orientation.portrait ? 2 : 3,
        	    children: List.generate(100, (index) {
	              return Center(
        	        child: Text("Item $index"),
	              );
        	    }),
	          );
        	}));
	  }
	}
```
2. `OrientationBuilder` works great with `GridView`. The app below will fetch some images from Unsplash API and show them in a GridView. Make sure to add `http:` to your `pubspec.yaml` file. Also, in order for this app to work, you need a developer account at Unsplash which is free to create. Please use your own Access Key for this app by creating an account and Unsplash application.

```
	import 'dart:convert';

	import 'package:flutter/material.dart';
	import 'package:http/http.dart';

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
	      appBar: AppBar(title: Text("Orientation Demo")),
	      body: FutureBuilder(
	        future: getImages(),
        	builder: (BuildContext context, AsyncSnapshot snapshot) {
	          if (!snapshot.hasData) {
        	    return Center(child: CircularProgressIndicator());
	          }
        	  return OrientationBuilder(builder: (context, orientation) {
	            return GridView.builder(
	                gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
	                  crossAxisCount: orientation == Orientation.portrait ? 2 : 3,
	                ),
	                itemCount: snapshot.data.length,
	                itemBuilder: (context, index) {
	                  return Container(
	                    child: Image.network(
	                      snapshot.data[index],
	                      fit: BoxFit.cover,
	                    ),
	                  );
	                });
	          });
	        },
	      ),
	    );
	  }
	
	  Future<List<String>> getImages() async {
	    String access_key = "YOUR_ACCESS_KEY_HERE";
	    final queryParameters = {'client_id': access_key};
	    var url = Uri.https("api.unsplash.com", "photos/", queryParameters);
	    var response = await get(url);
	    var data = jsonDecode(response.body);
	
	    List<String> imageURLs = [];
	
	    for (var item in data) {
	      imageURLs.add(item["urls"]["thumb"]);
	    }
	    return imageURLs;
	  }
	}
```
3. Orientation can be locked using SystemChrome. You need to `import 'package:flutter/services.dart';` before using `SystemChrome`
```
void initState() {
    super.initState();
		    SystemChrome.setPreferredOrientations(
		        [DeviceOrientation.portraitUp, DeviceOrientation.portraitDown]);
}
```	
