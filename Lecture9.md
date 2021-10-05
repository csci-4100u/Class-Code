# Scaffold Components in Flutter

**1. AppBar**  
Scaffold AppBar allows adding action buttons.

It is always recommended to keep your code clean and tidy by putting them in appropriate files, however, for this lecture, all the code is placed in a single `main.dart` file.

```
class MyHomePage extends StatelessWidget {
	  @override
	  Widget build(BuildContext context) {
	    return Scaffold(
	      appBar: AppBar(
	        title: Text("Scaffold App Demo"),
	        actions: [
	          IconButton(
	              onPressed: () {
	                ScaffoldMessenger.of(context).showSnackBar(
	                    SnackBar(content: Text("App Bar Cart Icon tapped")));
	              },
	              icon: Icon(Icons.shopping_cart)),
	          IconButton(
	              onPressed: () {
	                ScaffoldMessenger.of(context).showSnackBar(
	                    SnackBar(content: Text("App Bar Cart Icon tapped")));
	              },
	              icon: Icon(Icons.contact_page))
	        ],
	      ),
	    );
	  }
	}

```   
**2. PopupMenuButton**  
PopupMenuButton is used if more action buttons are required.  
The code below will be added either at the bottom of the above written code or as a separate file. The object of this class is then called as a child of `actions` in the AppBar.

```
class AppBarPopupMenu extends StatelessWidget {
	  @override
	  Widget build(BuildContext context) {
	    return PopupMenuButton(itemBuilder: (BuildContext context) {
	      return [
	        PopupMenuItem(child: Text("Refund")),
	        PopupMenuItem(child: Text("Voucher"))
	      ];
	    });
	  }
	}

```
**3. Floating Action Button**  
A Floating Action Button can be used to add a button to the screen.
The code below will be added either at the bottom of the above written code or as a separate file. The object of this class is then provided to `floatingActionButton` property of the Scaffold.

```
class MyFloatingButton extends StatelessWidget {
  Widget build(BuildContext context) {
    return FloatingActionButton(
        child: Icon(Icons.shopping_cart_outlined), onPressed: () {});
	  }
	}

```

**4. BottomNavigationBar**  
BottomNavigationBar is used for tapped bars at the bottom.
The code below will be added either at the bottom of the above written code or as a separate file. The object of this class is then provided to `bottomNavigationBar` property of the Scaffold.

```
class MyBottomNavigationBar extends StatefulWidget {
	  @override
	  _MyBottomNavigationBarState createState() => _MyBottomNavigationBarState();
	}

	class _MyBottomNavigationBarState extends State<MyBottomNavigationBar> {
	  int _currentIndex = 0;

	  @override
	  Widget build(BuildContext context) {
	    return BottomNavigationBar(
	      items: [
	        BottomNavigationBarItem(icon: Icon(Icons.list), label: "My List"),
	        BottomNavigationBarItem(
	            icon: Icon(Icons.account_balance), label: "My Account"),
	      ],
	      currentIndex: _currentIndex,
	      onTap: (int index) {
	        setState(() {
	          _currentIndex = index;
	        });
	      },
	    );
	  }
	}

```

**5. Drawer**  
Drawers are used for Sliding Menu from left.
The code below will be added either at the bottom of the above written code or as a separate file. The object of this class is then provided to `drawer` property of the Scaffold.

```
class MyDrawer extends StatelessWidget {
	  @override
	  Widget build(BuildContext context) {
	    return Drawer(
	      child: Column(
	        mainAxisAlignment: MainAxisAlignment.start,
	        crossAxisAlignment: CrossAxisAlignment.start,
	        children: []
		));
	}
	}

```