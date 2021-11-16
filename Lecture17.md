# Maps in Flutter

Add permission to Manifest file

	    <uses-permission android:name="android.permission.INTERNET"/>

Add packages to yaml file:

	  flutter_map: 
	  latlong:

`main.dart`
```
import 'package:flutter/material.dart';
import 'package:flutter_map/plugin_api.dart';
import 'package:latlong2/latlong.dart';

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
      appBar: AppBar(title: Text("Maps Demo")),
      body: ScaffoldBodyContent(),
    );
  }
}

class ScaffoldBodyContent extends StatelessWidget {
  final center = LatLng(43.9644879, -78.89896);
  @override
  Widget build(BuildContext context) {
    return FlutterMap(
      options: MapOptions(zoom: 16.0, center: center),
      layers: [
        TileLayerOptions(
            urlTemplate:
                "MAPBOX_URL_HERE",
            additionalOptions: {
              'accessToken':
                  'ACCESS_TOKEN_HERE',
              'id': 'mapbox.mapbox-streets-v8'
            }),
        MarkerLayerOptions(markers: [
          Marker(
              point: center,
              builder: (BuildContext context) {
                return IconButton(
                  onPressed: () {
                    showModalBottomSheet(
                        context: context,
                        builder: (BuildContext context) {
                          return bottomSheet();
                        });
                  },
                  icon: Icon(Icons.location_on),
                  iconSize: 30.0,
                  color: Colors.blueAccent,
                );
              }),
        ]),
        PolylineLayerOptions(polylines: [
          Polyline(color: Colors.blueAccent, strokeWidth: 2.0, points: [
            LatLng(43.9644879, -78.89896),
            LatLng(43.96444, -78.8986),
          ]),
        ]),
      ],
    );
  }

  Widget bottomSheet() {
    return Column(
      children: [
        Container(
          height: 100,
          color: Colors.blueAccent,
          child: ListTile(
            title: Text(
              "Ontario Tech University",
              style: TextStyle(color: Colors.white, fontSize: 20.0),
            ),
            subtitle: Text(
              "University",
              style: TextStyle(color: Colors.white70, fontSize: 14.0),
            ),
            trailing: Text(
              "25 mins",
              style: TextStyle(color: Colors.white, fontSize: 16.0),
            ),
          ),
        ),
        SizedBox(
          height: 10.0,
        ),
        Row(
          mainAxisAlignment: MainAxisAlignment.spaceAround,
          children: [
            IconButton(
              onPressed: () {},
              icon: Icon(Icons.call),
              color: Colors.blueAccent,
              iconSize: 35.0,
            ),
            IconButton(
              onPressed: () {},
              icon: Icon(Icons.share),
              color: Colors.blueAccent,
              iconSize: 35.0,
            ),
            IconButton(
              onPressed: () {},
              icon: Icon(Icons.save),
              color: Colors.blueAccent,
              iconSize: 35.0,
            ),
          ],
        ),
        Divider(
          thickness: 1.5,
        ),
        Row(
          children: [
            Expanded(
              child: ListTile(
                title: Text("2000 Simcoe Street North"),
                leading: Icon(
                  Icons.location_on,
                  color: Colors.blueAccent,
                ),
              ),
            ),
            Expanded(
              child: ListTile(
                title: Text("Open 8:00AM - 8:00PM"),
                leading: Icon(
                  Icons.location_on,
                  color: Colors.blueAccent,
                ),
              ),
            ),
          ],
        ),
      ],
    );
  }
}

```
