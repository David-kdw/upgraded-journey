![Logo DIT](img\Logo.png)
*KUDAWOO Séna Kodjovi*
# Special Method Names
## Contents
---
#### Introduction
#### Basic Concept
#### Theory
1. Classes That Act Like Iterators
2. Computed Attributes
3. Classes That Act Like Functions#
4. Classes That Act Like Sets
5. Classes That Act Like Dictionaries
6. Classes That Act Like Numbers
7. Classes That Can Be Compared
8. Classes That Can Be Serialized
9. Classes That Can Be Used in a with Block
#### Practical example 
#### Potential bypass
#### Use cases vs data analysis
#### Conclusion 
To learn more about

#### Introduction
As in every language of programmation, Python has its predefined classes as well as own classes can be defined. Classes have attributes, methods and **special methods - “magic” methods**. 
Using special methods, your classes can act like sets, like dictionaries, like functions, like iterators, or even like numbers. Let us explore their meaning, use, syntax and more...
#### Basic Concept
We recall that we have already used a special method __ init__()to initialize attributes of classes. This was in fact a magic method in the class. We can recognize a magic method inside a class by the edges __ "__(*dunder*) bordering the method name. 
There are alse other basic special methods to know for debugging your custom classes. they are as in the table below :
| You want | Write | And Python calls|
| --------------------------- | ---------------- |----------- |
| to initialize an instance | x = MyClass() |x = MyClass()|
| the “official” representation as a string| repr(x) or x | x.__ repr__()|
| the “informal” value as a string| str(x) | x.__ str__()|
| the value as a formatted string| format(x, format_spec)|x.__ format__(format_spec)|

An example to summarize is as follows : 
``` 
class Person():
    def __init__(self):
        self.fname = "Joe"
        self.lname = "Marini"
        self.age = 25
    # use __repr__ to create a string useful for debugging
    def __repr__(self):
        return "<Person Class - fname:{0}, lname:{1}, age{2}>".format(self.fname, self.lname, self.age)
    # use str for a more human-readable string
    def __str__(self):
        return "Person ({0} {1} is {2})".format(self.fname, self.lname, self.age)
    # use bytes to convert the informal string to a bytes object
    def __bytes__(self):
        val = "Person:{0}:{1}:{2}".format(self.fname, self.lname, self.age)
        return bytes(val.encode('utf-8'))
```
Now if we create a Person object and print it out using these functions:
```
   # create a new Person object
    cls1 = Person()
    # use different Python functions to convert it to a string
    print(repr(cls1))
    print(str(cls1))
    print("Formatted: {0}".format(cls1))
    print(bytes(cls1))
```
We will have the following output:
#<Person Class - fname:Joe, lname:Marini, age25>
#Person (Joe Marini is 25)
#Formatted: Person (Joe Marini is 25)
#b'Person:Joe:Marini:25'

#### Special Methods
In this section, we will see how to use some common magic methods that are important to know in our programming adventure along with python

##### Classes That Act Like Iterators
##### Theory 
__ iter__() and  __ next__() are called whenever you create a new itertor and retrievethe next value of the iterator. 
In Python, an iterator is an object that can be iterated upon. In simpler words, we can say that Iterators are objects that allow you to traverse through all the elements of a collection and return one element at a time. More specifically, we say that an iterator is an object that implements the iterator protocol.
Iterators are used in both **for loops** and **while loops**. Learn more with the help of this blog post. 
![ITER()](img\iter.JPG)

##### Practical Example
Here is a simple example, describing these methods:
 > Example 1 :
``` 
x =[1,2,3,4]
# get an iterator using iter()
a = x.__iter__()
#Get the first item
a.__next__()
1
#Get the second item
a.__next__()
2
```
> Example 2 :
``` 
# define an iterable such as a list
list1=[1,2,3,4,5,6,7,8,9,0]
# get an iterator using iter()
iter1=iter(list1)
# infinite loop
while True:
    try:
        # get the next item
        print(next(iter1))
        # do something with element
    except Stop:
        #  break from loop
        break
```
**Output:**
1
2
3
4
5
6
7
8
9
0


 

##### Computed Attributes
##### Theory 
Python provides a set of methods that classes can use to access the attributes of an object. Whenever we retrieve or set an object’s attributes, Python calls one of these functions to perform any desired processing. 

__ getattribute__() and __ getattr__(), are called to retrieve an attribute value. These are slightly different from each other. Getattr is called only when the requested attribute can’t be found on the object. Meanwhile, getattribute is called unconditionally every time an attribute name is requested. Additionally, there are __ setattr__, __ delattr__, and __ dir__() to set, delete and discover supported attributes
##### Practical Example
>Example
```
class myColor():
    def __init__(self):
        self.red = 50
        self.green = 75
        self.blue = 100
    # use getattr to dynamically return a value
    def __getattr__(self, attr):
        if attr == "rgbcolor":
            return (self.red, self.green, self.blue)
        elif attr == "hexcolor":
            return "#{0:02x}{1:02x}{2:02x}".format(self.red, self.green, self.blue)
        else:
            raise AttributeError
    # use setattr to dynamically return a value
    def __setattr__(self, attr, val):
        if attr == "rgbcolor":
            self.red = val[0]
            self.green = val[1]
            self.blue = val[2]
        else:
            super().__setattr__(attr, val)
    # use dir to list the available properties
    def __dir__(self):
        return ("rgbolor", "hexcolor")
```
The above code modifies the attribute related methods to get colour information. As user passes a supported attribute name, e.g. `rgbcolor`python will return the value corresponding to the name

```
# create an instance of myColor
cls1 = myColor()
# print the value of a computed attribute
print(cls1.rgbcolor)
#(50, 75, 100)
# same as you are doinf like this
print(cls1._getattribute__('rgbcolor))
#(50, 75, 100)
# or doing like this
getattr(cls1, 'rgbcolor')
print(cls1.hexcolor)
#(50, 75, 100)
#set attribute red at 100
cls1.rgbcolr = [100, 100, 100]
#same as 
cls1.__setattr__('rgbcolor', [100, 100, 100]) 
#delete an attribute 
del cls1.red
# same as 
cls1.__delattr__('red')
#To list all attributes and methods 
dir(cls1)
#same as 
cls1.__dir__()
```

##### Classes That Act Like Functions#
##### Theory 
##### Practical Example

##### Classes That Act Like Sets
##### Theory 
##### Practical Example

##### Classes That Act Like Dictionaries
##### Theory 
##### Practical Example

##### Classes That Act Like Numbers
##### Theory 
##### Practical Example

##### Classes That Can Be Compared
##### Theory 
##### Practical Example

##### Classes That Can Be Serialized
##### Theory 
##### Practical Example

##### Classes That Can Be Used in a with Block
##### Theory 
##### Practical Example

#### Use cases in data analysis
#### Conclusion 
To learn more about
# upgraded-journey
