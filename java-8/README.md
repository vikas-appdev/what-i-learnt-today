# Java 8 new features

### Interface default and static method
<p>Before java 8, interfaces could have only public abstract methods. It was not possible to add new functionality to the existing interface without forcing all implementation classes to create an implementation of the new methods nor it was possible to create interface methods with an implementation.</p>

<p>Starting with Java 8, interfaces can have static and default methods that, despitebeing declared in an interface, have a defined behavior.</p>

#### Static Method
<p>consider the following method of the interface.</p>

```java
static String helloStatic(){
	return "Hello from static method of interface.";
}
```

- The static helloStatic() method is available only through and inside of an interface. It can't be overridden by an implementing class.

- To call it outside the interface the standard approach for static method call should be used.

```java
String result = InterfaceName.helloStatic();
```


#### Default method 

<p>Default methods are declared using the new default keyword. These are accessible through the instance of the implementing class and can be overridden.</p> 

```java
default String defaultMethod(){
	return "Called from default method.";
} 
```

### Method reference 

<p>Method reference can be used as a shorter and more readable alternative for a lambda expression which only calls an existing method. There are four variants of method reference.</p>

#### Reference to a Static method 

<p>The reference to a static method holds the following syntax: ContainingClass::methodName.</p>
<p>Let's try to count all empty string in the `List<String>` with help of Stream API.</p>

```java
boolean isReal = list.stream().anyMatch(u-> User.isRealUser(u));
```

<p>Take a closer look at lambda expression in the anyMatch() method, it just makes a call to a static method isRealUser(User user) of the User class. So it can be substituted with a reference to a static method:</p>

```java
boolean isReal = list.stream().anyMatch(User::isRealUser);
```

This types of code looks much more informative.

#### Reference to an Instance method

<p>The reference to an instance method holds the following syntax: containingInstance::methodName. Following code calls method isLegalName(String string) of type User which validates an input parameter:</p>

```java
User user = new User();
boolean isLegalName = list.stream().anyMatch(user::isLegalName);
```

#### Reference to an Instance Method of an Object of a Particular Type

This reference method takes the following syntax: ContainingType::methodName. An example::
```java
long count = list.stream().filter(String::isEmpty).count();
```

#### Reference to a Constructor

A reference to a constructor takes the following syntax: ClassName::new. As constructor in Java is a special method, method reference could be applied to it too with the help of new as a method name.

```java
Stream<User> stream = list.stream().map(User::new);
```


### Optional<T>

Before Java 8 developers had to carefully validate values they referred to, because of a possibility of throwing the NullPointerException (NPE). All these checks demanded a pretty annoying and error-prone boilerplate code.

Java 8 Optional<T> class can help to handle situations where there is a possibility of getting the NPE. It works as a container for the object of type T. It can return a value of this object if this value is not a null. When the value inside this container is null it allows doing some predefined actions instead of throwing NPE.

#### Creation of the Optional<T>

An instance of the Optional class can be created with the help of its static methods:

```java
Optional<String> optional = Optional.empty();
```

Returns an empty Optional.

```java
String str = "value";
Optional<String> optional = Optional.of(str);
```

Returns an Optional which contains a non-null value.

```java
Optional<String> optional = Optional.ofNullable(getString());
```

Will return an Optional with a specific value or an empty Optional if the parameter is null.


#### Optional<T> Usage

For example, you expect to get a List<String> and in the case of null you want to substitute it with a new instance of an ArrayList<String>. With pre-Java 8's code you need to do something like this:

```java
List<String> list = getList();
List<String> listOpt = list != null ? list : new ArrayList<>();
```


With Java 8 the same functionality can be achieved with a much shorter code:

```java
List<String> listOpt = getList().orElseGet(() -> new ArrayList<>());
```

There is even more boilerplate code when you need to reach some object's field in the old way. Assume you have an object of type User which has a field of type Address with a field street of type String. And for some reason you need to return a value of the street field if some exist or a default value if street is null:

```java
User user = getUser();
if (user != null) {
    Address address = user.getAddress();
    if (address != null) {
        String street = address.getStreet();
        if (street != null) {
            return street;
        }
    }
}
return "not specified";
```

This can be simplified with Optional:

```java
Optional<User> user = Optional.ofNullable(getUser());
String result = user
  .map(User::getAddress)
  .map(Address::getStreet)
  .orElse("not specified");
```
  
 In this example we used the map() method to convert results of calling the getAdress() to the Optional<Address> and getStreet() to Optional<String>. If any of these methods returned null the map() method would return an empty Optional.

Imagine that our getters return Optional<T>. So, we should use the flatMap() method instead of the map():

```java
Optional<OptionalUser> optionalUser = Optional.ofNullable(getOptionalUser());
String result = optionalUser
  .flatMap(OptionalUser::getAddress)
  .flatMap(OptionalAddress::getStreet)
  .orElse("not specified");
```
  
  Another use case of Optional is changing NPE with another exception. So, as we did previously, let's try to do this in pre-Java 8's style:
```java  
String value = null;
String result = "";
try {
    result = value.toUpperCase();
} catch (NullPointerException exception) {
    throw new CustomException();
}
```

And what if we use Optional<String>? The answer is more readable and simpler:

```java
String value = null;
Optional<String> valueOpt = Optional.ofNullable(value);
String result = valueOpt.orElseThrow(CustomException::new).toUpperCase();
```


Notice, that how and for what purpose to use Optional in your app is a serious and controversial design decision, and explanation of its all pros and cons is out of the scope of this article. If you are interested, you can dig deeper, there are plenty of interesting articles on the Internet devoted to this problem. This one and this another one could be very helpful.


### Consumer Interface



<div align="center">

#### [Here you can find updated java-codes](https://github.com/vikas-appdev/the-java-codelab)

</div>


