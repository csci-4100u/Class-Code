# Camera in Flutter

1. Add `camera:` to `pubspec.yaml`

2. Make sure you have the following in `android > app > build.gradle`
```
    compileSDKVersion 30 
    minSDKVersion 21  
    targetSDKVersion 30  
```
`main.dart`
```
import 'dart:io';

import 'package:flutter/material.dart';
import 'package:camera/camera.dart';

List<CameraDescription> cameras = [];

Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  cameras = await availableCameras();
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
  late CameraController _controller;
  late Future<void> _initializeController;

  @override
  void initState() {
    super.initState();
    _controller = CameraController(cameras.first, ResolutionPreset.medium);
    _initializeController = _controller.initialize();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Camera Demo")),
      body: FutureBuilder(
        future: _initializeController,
        builder: (context, snapshot) {
          if (snapshot.connectionState == ConnectionState.done) {
            return CameraPreview(_controller);
          } else {
            return CircularProgressIndicator();
          }
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () async {
          var image = await _controller.takePicture();
          print(image.path);
          await Navigator.push(
              context,
              MaterialPageRoute(
                  builder: (context) => ImageViewer(image: image.path)));
        },
        child: Icon(Icons.camera),
      ),
    );
  }
}

class ImageViewer extends StatelessWidget {
  final String image;
  const ImageViewer({Key? key, required this.image}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Image Viewer"),
      ),
      body: Center(
        child: Image.file(File(image)),
      ),
    );
  }
}
```