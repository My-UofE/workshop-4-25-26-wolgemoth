[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/caRIFgDu)
[![Open in Codespaces](https://classroom.github.com/assets/launch-codespace-2972f46106e565e64193e422d61a12cf1da4916b45550586e14ef0a7c637dd04.svg)](https://classroom.github.com/open-in-codespaces?assignment_repo_id=22555090)
## ECM1410 Workshop 04 Instructions

Please accept the GitHub classroom Workshop 4 assignment from the ECM1410 ELE page, and open the repository in GitHub CodeSpaces.

You should find you have files `RectangleApp.java` and `Rectangle.java` in your working folder. Open the files and check you can understand the code. 

Compile the files in the terminal:

```
javac RectangleApp.java
```

Note that this should compile both `RectangleApp.java` and `Rectangle.java` producing two `.class` files.

Then, run the program with command:

```
java RectangleApp
```

Read through the code, and compare to the output. 

Make sure you understand how the program is working. Ask a member of the teaching team if you have any questions.

We will now work to edit and extend the example program using the techniques and ideas of object orientated programming covered in the lectures.

### Part 1. Accessing object attributes using `this` 

The `this` keyword can be used within a class definition to refer to the current class instance. 

An advantage of this is to distinguish between variables and attributes. 

For example suppose we 
wanted to be consistent throughout our code and use variable name `width` to store the width values. We might end up with ambiguous code like that below:

```java
public Rectangle(double width, double height, double originX, double originY) {
    width = width;
    ...
```

Here we end up with the confusing line: `width = width;` as we have used the same name for the rectangle width attribute and the width constructor argument.

The `this` keyword allows us to resolve the issue by letting us refer explicitly to instance attributes using code like `this.width` rather than the width attribute directly. With this change our code becomes:

```java
public Rectangle(double width, double height, double originX, double originY) {
    this.width = width;
    ...
```

**TASK** 

Update the `Rectangle.java` constructor to use argument names `width`, `height`, `originX` and `originY` as below. Make corresponding changes the constructor body setting attributes using the `this` keyword, to ensure the code functions as expected.

```java
public Rectangle(double width, double height, double originX, double originY) {
    ...
```

Recompile and run `RectangleApp.java`  to check your program still works.

**TASK** 

Overload the constructor by inserting the following code beneath the constructor you have been editing:

```java
// second constructor: 
public Rectangle(double width, double height) {
    this(width, height, 0, 0)
}
```

This constructor allows us to instantiate a rectangle without providing all four arguments (i.e. we only need to pass width and height, not origin co-ordinates).

To test out this constructor uncomment the block of code in `RectangleApp.java` that defines `myRect2` and displays its attributes. Check you understand how the default origin co-ordinates for rectangles created by this constructor are set.

**TASK** 

Add another constructor that allows the user to create a rectangle without providing any arguments, i.e. of form:

```java
// second constructor: 
public Rectangle() {
    ...
}
```

In this case its width and height should be set to 1, and its origin set to x=0, y=0.

Uncomment the code block that defines `myRect3` in `RectangleApp.java` to check your code.

Once you have completed this task commit and push your work with the message:

```
completed part 1
```

### Part 2. Adding more methods

#### 2.1 Scaling the rectangles

Suppose we want to scale the rectangle. 

e.g. 

We could scale it by `x2` in both the x and y directions so that we  double its height and width. 

We could scale it by `x3` in the y-direction only so that we triple its height.

We could scale it by `x0.5` in the x-direction only so that we reduce its width by half.

**TASK**

Create an additional method `scale` that can implement this.

You should overload the method so that it can be called in two ways:

i) by providing two scaling factors (`scaleX` and `scaleY` to be applied to the width and height respectively).

ii) by providing a single scaling factor (to be applied to both width and height).
 
 
**Hint.** Look at the `move` method as an example if you are unsure of how to go about this.

 Test your methods by adding the following lines of code at the bottom of `RectangleApp.java` and adding additional code to display the new dimensions of the rectangles.

```java
 myRect1.scale(0.5); // applies 0.5 scale to both x and y, changing width to 8, height to 4

 myRect2.scale(1,3); // should change height to 24 with width unchanged

 myRect3.scale(15,10); // should scale to width 15, height 10
```

#### 2.2 Comparing rectangle positions

Suppose we have two rectangle objects. We might want to determine if they overlap.

We can do this with a method taking the following form:

```java
public boolean isOverlappedWith(Rectangle r){]
   ...
}
```

For example, when completed we could then check if rectangle `myRect1` overlaps `myRect2` using:

```java
boolean overlapping = myRect1.isOverlappedWith(myRect2);
```

Within the `isOverlappedWith` method we can use the attributes of `this` and `r` to compare the positions of the two rectangles. 

Edit your code to add this method. When you have finished you can test it on the following rectangles.

```java
Rectangle myRect4 = new Rectangle(30.0, 5.0, 10, 10); 
Rectangle myRect5 = new Rectangle(50.0, 20.0, 0, 0); 
Rectangle myRect6 = new Rectangle(20.0, 40.0, 500, 500); 

// myRect4 overlaps myRect5 so these should show as true
System.out.println( "myRect4 overlaps myRect5: " + myRect4.isOverlappedWith(myRect5) ) ; 
System.out.println( "myRect5 overlaps myRect4: " + myRect5.isOverlappedWith(myRect4) ) ;

// myRect4 does not overlap myRect6 so these should show as false
System.out.println( "myRect4 overlaps myRect6: " + myRect4.isOverlappedWith(myRect6) ) ;
System.out.println( "myRect6 overlaps myRect4: " + myRect6.isOverlappedWith(myRect4) ) ;
```

**HINT**

<img src="./overlapping_rectangles.png"></img>

We could also write a function to check if two rectangles overlap using a static method, which can be called by passing the two arguments you wish to compare, i.e. with method definition:

```java
public static boolean areOverlapping(Rectangle r1, Rectangle r2)
```

and is used using code like:

```java
boolean result = Rectangle.areOverlapping(myRect4, myRect5);
System.out.println( "myRect4 overlaps myRect5: "+result);
```

Add this method to your code. Note rather than duplicate the code that calculates whether they overlap, you should call the previous method `isOverlappedWith`. Ask for help if you are unsure how to do this.

#### 2.3 Finding the aspect ratio

 - Add a method calcRatio() for calculating the ratio of width to height.

 - Add a method isSquare() for determining if the rectangle is square or not.

Note: use the correct way of testing floating-point numbers for equality, as practiced in the first workshop, e.g. define a square as having ratio is within the range 0.999 and 1.001

Once you have completed this task commit and push your work with the message:

```
completed part 2
```

### Part 3. The access modifier

As mentioned in the lecture, a well-encapsulated class always hide their attributes to avoid the object’s state (or attributes) being directly changed outside of the class. 

To achieve this we need set all the instance attributes to private, and provide public setter and getter methods to modify and view the attributes.

**TASK**

Edit the Rectangle.java file so that the Rectangle class is well-encapsulated.

As an example, to update the `width` attribute we would change the line:

```java
// original line:
public double width;
```

so that the attribute is private:

```java
// becomes
private double width; 
```

Then add public methods to get and set the attribute:

```java
// for each attribute provide getter method
public double getWidth(){ 
  return width;
}
```

```java
// for each attribute provide setter method
public void setWidth(double width){
  this.width = width;
}
```

When you think you have completed this, try to compile `Rectangle.java` (not `RectangleApp.java`) and work through any issues that are flagged.

When `Rectangle.java` compiles successfully you can then try to compile `RectangleApp.java`. This will now fail because it needs to ne updated in line with the changes to the rectangle class. In particular we must edit the code so we use the getter/setter methods to access attributes. 

Update the code accordingly, until both files compile and run correctly.

**TASK**

An advantage of this method is that it allows us to perform checks or validation when attributes are updated. For example we might want to prevent the `height` and `width` taking negative values.

Update the `setWidth` and `setHeight` methods so that the `width` and `height` would be unchanged if they are used with a negative value. Test your code by adding the following example to the `RectangleApp.java` file:

```java
System.out.println("Check class prevents negative widths");

// initialise rectangle for test
Rectangle myRect7 = new Rectangle(30.0, 5.0, 10, 10); 
System.out.println( "Width: "+myRect7.getWidth()+", Height: "+myRect7.getHeight() );

// change to positive width should be allowed
myRect7.setWidth(40);
System.out.println( "Width: "+myRect7.getWidth()+", Height: "+myRect7.getHeight() );

// change to negative width should be ignored
myRect7.setWidth(-10);
System.out.println( "Width: "+myRect7.getWidth()+", Height: "+myRect7.getHeight() );
```

Once you have completed this task commit and push your work with the message:

```
completed part 3
```

### Part 4. Object reference

 Add code to the bottom of RectangleApp to create three rectangles as follows.

```java
Rectangle r1 = new Rectangle(10.0,5.0);
Rectangle r2 = new Rectangle(10.0,5.0);
Rectangle r3 = r2;
```

Then use println() to print the three rectangle's 'value'.

```java
System.out.println("Object reference tests:");
System.out.println("r1: " + r1);
System.out.println("r2: " + r2);
System.out.println("r3: " + r3);
```

When run the program, you will see the output like this: `Rectangle@7852e922`, which is the class name together with the hashcode of the object in hexadecimal (you may understand it as the memory address for each object). 

You should see the hashcode of `r1` and `r2` are different, because whenever you `new` an object, the compiler will allocate a new block of memory for it.

However you should see that `r2` and `r3` have the same hash code. This is because the variable `r3` was assigned using `r3 = r2` so that it `r2` and `r3` reference the same object in memory. 

This means that whenever you change any attribute’s value for one object, the other object’s attribute value also changes. 

In other words, you may treat them as one object, but with two handles (`r2` and `r3`). 

Try adding the following statement:

```java
r2.scale(0.5);
System.out.println("r2 width: " + r2.getWidth());
System.out.println("r3 width: " + r3.getWidth());
```

Now rerun the program and check that the width of `r2` and `r3` were both updated.

Once you have completed this task commit and push your work with the message:

```
completed part 4
```

### Part 5. `toString()` method

Every well-designed Java class should contain a public method called `tostring()` that returns a short description of the instance (in a return type of `String`). 

The `toString()` method can be called explicitly (via `objectName.toString()`) just like any other method; or implicitly through `println()` or `print()`. 

If an instance is passed to the `println(objectName)` function, the `toString()` method of that instance will be invoked implicitly. 

Add the following `toString()` method to the Rectangle class:

```java
// Return a description of a rectangle in the form of
// Rectangle[x=*,y=*,w=*,h=*]
public String toString(){
return "Rectangle[x="+originX+",y="+originY+",w="+width+",h="+height+"]";
}
```

Re-compile and re-run `RectangleApp.java`, and you should see the outputs of the following statements are now updated.

```java
System.out.println("r1: " + r1);
System.out.println("r2: " + r2);
System.out.println("r3: " + r3);
```

This is because if a class doesn’t have the `toString()` method, the compiler will output the default `className@hashcode`, but if a class has a `toString()` method defined, the compiler will use that to when a print command is used.

Note you may call `toString()` method explicitly, just like any other methods, e.g.

```java
System.out.println("r1: " + r1.toString());
```

Once you have completed this task commit and push your work with the message:

```
completed part 5
```

### Part 6. Circles

You have worked to define a Rectangles class in an object-orientated way.  Let's now practise further by defining a `Circle` class.

You should create two files:

 - `Circle.java` containing the Circle class definition
 - `CircleApp.java` containing the `main()` method. Use this file to create some example objects and test out your methods.
 
You should code the following attributes, methods and constructors in the `Circle` class.

**Attributes:** (all set to be ’private’)

 - `radius`
 - `originX`
 - `originY`

**Constructors**

 - `Circle()` constructor with three arguments (radius and originX, originY)
 - `Circle()`  constructor with one argument (radius) defaults to origin at (0,0)
 - `Circle()` constructor with no arguments, defaults to radius 1 and origin at (0,0)

**Methods**

 - `getRadius` / `setRadius` (should disallow negative values)
 - `getOriginX` / `setOriginX`
 - `getOriginY` / `setOriginY`

 - `getArea`: Compute the area
 - `getCircumference`: Compute the circumference.
 - `move`: Move the circle 
 - `toString`: Describe the basic information of a circle by defining the toString() method.
 - `scale`: Scale the circle by a factor.
 - `isOverlappedWith`: Determine if a circle is overlapped with another circle. 
 - `isEnclosedBy`: Determine if one circle is enclosed within another circle. 
 

Ensure that your `Circle.java` and `CircleApp.java` files compile, and that you test out the class methods fully in your `CircleApp.java` file.

Once you are happy with your work commit and push your work with the message:

```
completed part 6
```
