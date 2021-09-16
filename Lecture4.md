# Dart OOP

**1. Defining Classes**  
	Classes in Dart are very similar to Classes in other programming languages like C++ and Java.

	class Login {
	  String UserName = '';
	  String Password = '';

	  Login();

	  @override
	  String toString() {
	    return "UserName: $UserName, Password: $Password";
  		}
	}

	void main() {
	  final user = Login();
	  user.UserName = "Razi";
	  user.Password = "UoIT";
	  print(user);
	}

**2. Long-Form Constructors**  
	You can use Long-Form Constructors just like other programming languages in Dart.

	class Login {
	  String UserName = '';
	  String Password = '';

	  //Long-Form Constructor
	  Login(String UserName, String Password) {
	    this.UserName = UserName;
	    this.Password = Password;
	  }


	  @override
	  String toString() {
	    return "UserName: $UserName, Password: $Password";
	  }
	}

	void main() {
	  final user = Login("Razi", "UoIT");
	  print(user);
	}

**3. Short-Form Constructor**  
	You can use Short-Form Constructors that use this keyword in the parameter of the constructor which is just a short form of writing it.

	class Login {
	  String UserName = '';
	  String Password = '';

	  //Short-Form Constructor
	  Login(this.UserName, this.Password);

	  @override
	  String toString() {
	    return "UserName: $UserName, Password: $Password";
	  }
	}

	void main() {
	  final user = Login("Razi", "UoIT");
	  print(user);
	}

**4. Private Members**  
	You can put an _ to make a variable private. They can still be accessed from main if main and class are in the same file.

	class Login {
	  String _UserName = '';
	  String _Password = '';

	  //Short-Form Constructor
	  Login(this._UserName, this._Password);

	  @override
	  String toString() {
	    return "UserName: $_UserName, Password: $_Password";
	  }
	}

**5. Inheritance**  
	Dart supports inheritance.

	class Vehicle {
 	 String Name = '';
	  String Type = '';
	  int KMs = 0;

	  Vehicle(this.Name, this.Type, this.KMs);

	  @override
	  String toString() {
	    return "Name: $Name, Type: $Type, KM: $KMs";
	  }
	}

	class Car extends Vehicle {
	  String carType = '';

	  Car(Name, Type, KMs) : super(Name, Type, KMs);

	  @override
	  String toString() {
	    return "Name: $Name, Type: $Type, KMs: $KMs, CarType: $carType";
	  }
	}

	class Truck extends Vehicle {
	  int LoadingCapacity = 0;

	  Truck(Name, Type, KMs) : super(Name, Type, KMs);

	  @override
	  String toString() {
	    return "Name: $Name, Type: $Type, KMs: $KMs, Loading Capacity: $LoadingCapacity";
	  }
	}

	void main() {
	  final corolla = Car("Corolla", "Car", 1000);
	  corolla.carType = "Sedan";
	  final loadingTruck = Truck("Nissan", "Truck", 1000);
	  loadingTruck.LoadingCapacity = 500;
	  print(corolla);
	  print(loadingTruck);
	}

**6. Mixins**  
	Mixins in Dart are good to add extra functionality to class which cant be done using multiple inheritance

	class Calculator with Adder, Subtractor {}

	mixin Adder {
	  void sum(int number1, int number2) {
	    print("Sum: ${number1 + number2}");
	  }
	}

	mixin Subtractor {
	  void subtract(int number1, int number2) {
	    print("Sum: ${number1 - number2}");
	  }
	}

	void main() {
	  Calculator cal = Calculator();
	  cal.sum(5, 6);
	  cal.subtract(6, 5);
	}

**7. Asynchronous and Synchronous**  
	Dart is single-threaded means only one main thread works at a time. An Event queue is maintained for any asynchronous tasks.  
	For Asynchronouos tasks, Future are used in Dart just like Promises are used in JS.


	void main() {
	  print('Before the delay');
	  Future myFuture = Future.delayed(Duration(seconds: 2), () => print('Inside delayed'));
	  print('After the delay statement');
	}  
	
In some cases you might want to block everything before future returns a value. In that case Awaits and Async can be used.

	Future<void> main() async {
	  print('Before the future');
	  final value = await Future<int>.delayed(
	    Duration(seconds: 2), () => 42, );
	  print('Value: $value');
	  print('After the future');
	}