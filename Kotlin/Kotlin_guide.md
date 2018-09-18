## Kotlin Summary
### class and inheritance
1. constructor
  primary constructor
  secondary constructor
2. creating instances of class
  creating instances of nested, inner and anonymous inner classes
3.class members
  classes can contain:
  Constructors and initializer blocks
  Functions
  Properties
  Nested and Inner Classes
  Object Declarations
 
 4. inheritance
 all classes in Kotlin have a common superclass Any
 
 keywords:
 open
 final [By default, all classes in Kotlin are final]
 override
  overriding properties  [attention to the initial orders,the base class will init in the first step.]
  Inside an inner class, accessing the superclass of the outer class is done with the super keyword qualified with the outer class name: super@Outer
 abstract
 
 5. companion objects
  In Kotlin, unlike Java or C#, classes do not have static methods. In most cases, it's recommended to simply use package-level functions instead.

  If you need to write a function that can be called without having a class instance but needs access to the internals of a class (for example, a factory method), you can write it as a member of an object declaration inside that class.

  Even more specifically, if you declare a companion object inside your class, you'll be able to call its members with the same syntax as calling static methods in Java/C#, using only the class name as a qualifier.
  
  ### declaring properties
  var 
  val
  
  The full syntax for declaring a property is:
  var <propertyName>[: <PropertyType>] [= <property_initializer>]
    [<getter>]
    [<setter>]
  
  field
  The field identifier can only be used in the accessors of the property.
  
  const
  compile-Time Constants.
  
  late-Initialized Properties and Variables
  
  
