# Charts in Flutter

In order to use charts in flutter, add `charts_flutter` to `pubspec.yaml`

`main.dart`
```
import 'package:flutter/material.dart';
import 'package:flutter_charts_2/world_population.dart';
import 'package:charts_flutter/flutter.dart';

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
	      length: 4,
	      child: Scaffold(
	        appBar: AppBar(
	          title: Text("Charts Demo"),
	          bottom: TabBar(
	            tabs: [
	              Tab(
	                child: Text("Bar"),
	              ),
	              Tab(
	                child: Text("Pie"),
	              ),
	              Tab(
	                child: Text("Line"),
	              ),
	              Tab(
	                child: Text("Scatter"),
	              ),
	            ],
	          ),
	        ),
	        body: TabBarView(
	          children: [
	            BarChartWidget("BarChart"),
	            BarChartWidget("PieChart"),
	            LineChartWidget(),
	            ScatterWidget(),
	          ],
	        ),
	      ),
	    );
	  }
	}

	class BarChartWidget extends StatelessWidget {
	  List<WorldPopulation> data = [
	    WorldPopulation("2020", 100000),
	    WorldPopulation("2019", 90000),
	    WorldPopulation("2018", 80000),
	    WorldPopulation("2017", 70000),
	    WorldPopulation("2016", 60000),
	  ];
	
	  String type = "";
	
	  List<Series<WorldPopulation, String>> listSeries = [];
	
	  BarChartWidget(String chartType) {
	    listSeries = [
	      Series(
	          id: "WorldPopulation",
	          data: data,
	          domainFn: (WorldPopulation population, _) => population.year,
	          measureFn: (WorldPopulation population, _) => population.population)
	    ];
	
	    type = chartType;
	  }
	
	  @override
	  Widget build(BuildContext context) {
	    if (type == "PieChart") {
	      return PieChart(listSeries);
	    }
	    return BarChart(listSeries);
	  }
	}
	
	class LineChartWidget extends StatelessWidget {
	  List<Sales> lstSales = [
	    Sales(1, 5000),
	    Sales(2, 7000),
	    Sales(3, 2000),
	    Sales(4, 8000),
	    Sales(5, 9000),
	    Sales(6, 7000),
	  ];

	  List<Series<Sales, int>> seriesList = [];
	
	  LineChartWidget() {
	    seriesList = [
	      Series(
	          id: "Sales",
	          data: lstSales,
	          domainFn: (Sales s, _) => s.year,
	          measureFn: (Sales s, _) => s.sales)
	    ];
	  }
	
	  @override
	  Widget build(BuildContext context) {
	    return LineChart(seriesList);
	  }
	}
	
	class ScatterWidget extends StatelessWidget {
	  List<Sales> lstSales = [
	    Sales(1, 5000),
	    Sales(2, 7000),
	    Sales(3, 2000),
	    Sales(4, 8000),
	    Sales(5, 9000),
	    Sales(6, 7000),
	  ];
	
	  List<Series<Sales, int>> seriesList = [];
	
	  ScatterWidget() {
	    seriesList = [
	      Series(
	          id: "Sales",
	          radiusPxFn: (Sales s, _) => 10,
	          data: lstSales,
	          domainFn: (Sales s, _) => s.year,
	          measureFn: (Sales s, _) => s.sales)
	    ];
	  }
	
	  @override
	  Widget build(BuildContext context) {
	    return ScatterPlotChart(seriesList);
	  }
	}

	class Sales {
	  int year;
	  int sales;

	  Sales(this.year, this.sales);
	}
```

`WorldPopulation.dart`

```
class WorldPopulation {
  String year;
  int population;

  WorldPopulation(this.year, this.population);

  @override
  String toString() {
    return "WorldPopulation($year, $population)";
  }
}

```