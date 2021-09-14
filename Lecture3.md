# Dart Basics
**1. Dart Programming Language Overview**  
    Dart is similar to other programming languages like C, C++ and Java. It is Statically Typed means variables types are known at compile time. It can use Type inference to know the type of variables at run time so var can be used.

**2. Variables in Dart**
	
	void main() 
	{
  	  String name = 'Razi';
	  int number = 10;
	  bool flag = true;
	  double decimal = 12.5;
	  var myVariable = 7;
	  dynamic anotherVariable = 10;

	  print('Name:  $name');
	  print('Number:  $number');
	  print('Flag:  $flag');
	  print('Decimal:  $decimal');
	  print('MyVariable:  $myVariable');
	  print('AnotherVariable:  $anotherVariable');

	  anotherVariable = 'Hello World';
 	  print('AnotherVariable:  $anotherVariable');
	}

**3.Commenting in Dart**  
	Commenting is similar to C++ and Java.

	Single Line comments:
	// dynamic anotherVariable = 10;

	Multi Line comments:
	  /*print('Name:  $name');
  	    print('Number:  $number');
 	    print('Flag:  $flag');
 	    print('Decimal:  $decimal');
	  */

**4. Operators in Dart**

	void main() {
  	    int number1 = 10;
 	    int number2 = 5;

	    //arithematic operators
	    var result = number1 * number2;

	    print('Result: $result');

	    // comparison operators
	    print(10 == 10);
	    print(10 != 10);
        print(5 > 6);
        print(6 < 8);
        print(6 <= 8);

        int i = 7;
        i++;
        print("i: $i");

        i--;
        print("i: $i");

        //logical operators
        print((5 <= 5) && (5 > 4));
        print((5 <= 5) || (5 > 4));

        //Negation operator
        print(!((5 <= 5) || (5 > 4)));
    }


**5. Final and Const**

	void main() {
        const double pi = 3.14;
        print("pi: $pi");

        // values of const variables cant be changed.
        // These values are assigned at compile time.
        //pi = 3.14786;

        // better to use final if values are not known at compile time.
        final String name;
        name = 'John';
        print('Name: $name');
    }


**5. if Statements**

	void main() {
        int number = 6;

        if (number % 2 == 0) 
        {
            print("Number is even");
        } 
        else 
        {
            print("Number is odd");
        }
	}

	/* You can also use ternary operators and switch statements in dart.*/


**6. Loops**

    // for loop
	void main() {
        for (int i = 0; i <= 10; i++) 
        {
            print(i);
        }
	}

	// while loops are also available
	void main() {
        int i = 1;
        while (i <= 10) 
        {
            print(i);
            i++;
        }
	}
    //	Similarly, a do-while loop can be used.

**7. Lists**

	void main() {
        List fruits = ["Apple", "Banana", "Grapes", "Oranges"];
        fruits.add("Pineapple");
        fruits.remove("Apple");

        final cars = ["Toyota", "Honda", "Suzuki"];
        cars.add("BMW");
        print(cars[3]);
	}

	void main() {
        List fruits = ["Apple", "Banana", "Grapes", "Oranges"];

        for (final fruit in fruits) 
        {
            print("I love $fruit");
        }
	}

**8. Map**

	void main() {
        Map<String, int> FruitBasket = {
            "Apple": 2,
            "Banana": 1,
            "Oranges": 3,
        };

        print("There are ${FruitBasket['Apple']} apples");
	}

	//keys and values attributes can be used for more details

	void main() {
        Map<String, int> FruitBasket = {
            "Apples": 2,
            "Banana": 1,
            "Oranges": 3,
        };

        FruitBasket["Strawberry"] = 5;
        FruitBasket.remove("Apples");

        for (var fruits in FruitBasket.keys) 
        {
            print("There are ${FruitBasket[fruits]} $fruits");
        }
	}


**9. Functions**

	bool isEven(int number) {
        bool flag = false;

        if (number % 2 == 0) {
            flag = true;
        }
        return flag;
	}

	void main() {
        if (isEven(5)) {
            print("Number is Even");
        } else {
            print("Number is Odd");
        }
	}

	//Optional Arguments

	void displayStudentInfo(String FirstName, String LastName, [String MiddleName = "NA"]) {
        print("First Name: $FirstName");
        print("Middle Name: $MiddleName");
        print("Last Name: $LastName");
	}

	void main() {
	    displayStudentInfo("Razi", "Iqbal");
	}

	//NamedParameters

	void displayStudentInfo({String FirstName = "NA", String LastName = "NA", String MiddleName = "NA"}) 
	{
        print("First Name: $FirstName");
        print("Last Name: $LastName");
	}

	void main() 
	{
	    displayStudentInfo(FirstName: "Razi", LastName: "Iqbal");	
	}


	//Anonymous Functions

	void main() {
        final Name = () {
            print("Razi");
        };

        Name();
	}

	//Similarly, parameters can be provided as well

	void main() 
	{
        var EvenOdd = (n) 
        {
            if (n % 2 == 0) 
            {
            return "Even";
                } 
            else 
            {
            return "Odd";
            }
        };

        print(EvenOdd(4));
	}

	//using Anonymous functions in loops for collections

	void main() 
	{
  		List numbers = [1, 2, 3, 4, 5];

		  numbers.forEach((element) 
		  {
		     print(element * element);
		  });
	}

	//Another variation would be to display only even numbers

	void main() 
	{
        List numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

        numbers.forEach((element) 
        {
            if (element % 2 == 0) 
            {
            print(element);
            }
        });
	}

	/* An arrow function can be used if there is only one line in the function body  */

	void main() 
	{
        var add = (int a, int b) => a + b;

        print(add(5, 4));
	}