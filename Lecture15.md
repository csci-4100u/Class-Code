# DataTable in Flutter

DataTables are used to show data in the form of a grid or table.

`main.dart`
```
import 'package:flutter/material.dart';
import 'grades.dart';

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
	      appBar: AppBar(title: Text("Data Table Demo")),
	      body: ScaffoldBodyContent(),
	    );
	  }
	}

	class ScaffoldBodyContent extends StatelessWidget {
	  @override
	  Widget build(BuildContext context) {
	    return DataTableWidget();
	  }
	}

	class DataTableWidget extends StatefulWidget {
	  const DataTableWidget({Key? key}) : super(key: key);

	  @override
	  _DataTableWidgetState createState() => _DataTableWidgetState();
	}

	class _DataTableWidgetState extends State<DataTableWidget> {
	  List<Grades> grades = [
	    Grades("1000001", "A"),
	    Grades("1000002", "B"),
	    Grades("1000003", "C"),
	    Grades("1000004", "D"),
	    Grades("1000005", "F"),
	    Grades("1000006", "A"),
	    Grades("1000007", "A"),
	    Grades("1000008", "C"),
	    Grades("1000009", "D"),
	    Grades("1000010", "A"),
	  ];

	  @override
	  Widget build(BuildContext context) {
	    return DataTable(
	      sortColumnIndex: 0,
	      sortAscending: true,
	      columns: [
	        DataColumn(
	            label: Text("Student ID"),
	            onSort: (i, b) {
	              grades.sort((a, b) => a.sid.compareTo(b.sid));
	            }),
	        DataColumn(
	            label: Text("Grade"),
	            onSort: (i, b) {
	              grades.sort((a, b) => a.grade.compareTo(b.grade));
	            })
	      ],
	      rows: grades
	          .map((e) => DataRow(cells: [
	                DataCell(Text(e.sid)),
	                DataCell(Text(e.grade)),
	              ]))
	          .toList(),
	    );
	  }
	}
```

`grades.dart`

```
class Grades {
  String sid;
  String grade;

  Grades(this.sid, this.grade);

  @override
  String toString() {
    return "Grades($sid, $grade)";
  }
}

```