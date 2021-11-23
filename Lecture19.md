# Internationalization in Flutter

1. Add the following into `pubspec.yaml` under dependencies
```
flutter_localizations:
    sdk: flutter
```
2. Add the following link to `flutter` in `pubspec.yaml`
```
generate: true
```
3. create a new yaml file `l10n.yaml`. Add the following lines to it
```
arb-dir: assets/l10n/
template-arb-file: app_en.arb
ouput-localization-file: app_localizations.dart
```
4. Create a new directory `assets/l10n/` and add the following files to it:
```
app_en.arb
app_ja.arb
```
5. Inside `app_en.arb`, add the following text:
```	
{
	 "language": "English",
	   "@language": {
   	     "description": "Default language"
  	  },
  	  "hello": "Hello World",
  	  "@hello": {
  	      "description": "Hello World Message"
 	   },
 	   "helloByName": "Hello {name}",
 	  "@helloByName": {
  	      "description": "Hello by name",
    	    "placeholders": {
  	          "name": {
     		           "type": "String"
       	     }
     	   }
  	  },
  	  "enterYourName": "Enter your name",
 	   "@enterYourName": {
   	     "description": "Enter your name"
 	   }
}
```
6. Inside `app_ja.arb`, add the following text:
```
{
    "language": "日本語",
     "hello": "ハローワールド",
     "helloByName": "こんにちは {name}",
      "enterYourName": "してください"
}
```
7. Run the app to generate `flutter_gen / gen_l10n` folders with the following files:
```
app_localizations_en.dart
app_localizations_ja.dart
app_localizations.dart
```
`main.dart`
```
import 'package:flutter/material.dart';
import 'package:flutter_localizations/flutter_localizations.dart';
import 'package:flutter_gen/gen_l10n/app_localizations.dart';

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
      supportedLocales: [
        Locale('en'),
        Locale('ja'),
      ],
      localizationsDelegates: [
        AppLocalizations.delegate,
        GlobalMaterialLocalizations.delegate,
        GlobalCupertinoLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
      ],
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Internationalization Demo")),
      body: ScaffoldBodyContent(),
    );
  }
}

class ScaffoldBodyContent extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Center(
        child: Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Text(
          AppLocalizations.of(context)!.language,
          style: TextStyle(fontSize: 30.0),
        ),
        Text(
          AppLocalizations.of(context)!.hello,
          style: TextStyle(fontSize: 22.0),
        ),
        Text(
          AppLocalizations.of(context)!.helloByName("Razi"),
          style: TextStyle(fontSize: 22.0),
        ),
        TextField(
          decoration: InputDecoration(
              labelText: AppLocalizations.of(context)!.enterYourName),
        )
      ],
    ));
  }
}
```