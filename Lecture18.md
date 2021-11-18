# Geolocation and Geocoding in Flutter

1. Make sure to have the following in build.gradle

	`compileSdkVersion 31`

	`minsdKVersion 21`  
	`targetSdkVersion 30`

2. Add following permissions in AndroidManifest
```
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />

<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />

<uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />

<uses-permission android:name="android.permission.INTERNET"/>
```
3. Add following packages in `pubspec.yaml`
```
geolocator: ^7.7.1
geocoding: 
```
4. main.dart
```
	import 'package:flutter/material.dart';
	import 'package:geolocator/geolocator.dart';
	import 'package:geocoding/geocoding.dart';

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

	class MyHomePage extends StatefulWidget {
	  @override
	  _MyHomePageState createState() => _MyHomePageState();
	}

	class _MyHomePageState extends State<MyHomePage> {
	  Geolocator geolocator = Geolocator();

	  String _currentLocation = '';
	  String _address = '';
	  double lat = 0.0, long = 0.0;
	
	  @override
	  Widget build(BuildContext context) {
	    _checkPermissions();
	    return Scaffold(
	      appBar: AppBar(title: Text("Geolocation Demo")),
	      body: Center(
	        child: Column(
	          mainAxisAlignment: MainAxisAlignment.center,
	          children: [
	            Text(_currentLocation),
	            Text(_address),
	          ],
	        ),
	      ),
	      floatingActionButton: Row(
	        mainAxisAlignment: MainAxisAlignment.end,
	        children: [
	          FloatingActionButton(
	            onPressed: () async {
	              var position = await _checkPermissions();
	              setState(() {
	                print(position);
	                _currentLocation =
	                    "Position(${position.latitude}, ${position.longitude})";
	                lat = position.latitude;
	                long = position.longitude;
	              });
	            },
	            child: Icon(Icons.update),
	          ),
	          FloatingActionButton(
	            onPressed: () async {
	              var position = await _checkPermissions();
	              setState(() {
	                print(position);
	
	                getAddress(position.latitude, position.longitude);
	              });
	            },
	            child: Icon(Icons.update_sharp),
	          ),
	        ],
	      ),
	    );
	  }
	
	  Future<Position> _checkPermissions() async {
	    LocationPermission permission;
	
	    permission = await Geolocator.checkPermission();
	
	    Geolocator.requestPermission();
	
	    return await Geolocator.getCurrentPosition(
	        desiredAccuracy: LocationAccuracy.best);
	  }
	
	  getAddress(double latitude, double longitude) async {
	    List<Placemark> places =
	        await placemarkFromCoordinates(latitude, longitude);
	
	    _address =
	        "Address: ${places.first.street}, ${places.first.locality}, ${places.first.country}, ${places.first.postalCode}";
	  }
	
	}
```