# upgraded-journey
![Logo DIT](img\Logo.png)

*By KUDAWOO Séna Kodjovi_Master1 IA DIT(Dakar)*
# Special Method Names
>> ## Contents
---
### Introduction
### Basic Concept of Special Methods
### Other special Method : Theory and Practical examples
1. Classes That Act Like Iterators
2. Computed Attributes
3. Classes That Act Like Functions
4. Classes That Act Like Sets
5. Classes That Act Like Dictionaries
6. Classes That Act Like Numbers
7. Classes That Can Be Compared
8. Classes That Can Be Serialized
9. Classes That Can Be Used in a with Block
### Potential bypass
### Use cases vs data analysis
### Conclusion 
  - To learn more about

---
>> ## Introduction
---
As in every language of programmation, Python has its predefined classes as well as own classes can be defined. Classes have attributes, methods and **special methods - “magic” methods**. 

In this section, we will learn about a variety of instance methods that are reserved by Python, which affect an object’s high level behavior and its interactions with operators. These are known as special methods.
Using special methods, your classes can act like sets, like dictionaries, like functions, like iterators, or even like numbers. Let us explore their meaning, use, syntax and more...

---
>> ## Basic Concept of Special Methods
---
We will recall that we have already used a special method named *__ init__()* to initialize attributes of classes and controls the process of creating instances of a class. This was in fact a magic method in the class. 

Generally, we can recognize a magic method inside a class by the edges __ "__(*dunder* double underscore) bordering the method name. Some basic ones to know for debugging a custom class are as follow : 
| Method | Explanation | Signature under the hood|
| --------------------------- | ---------------- |----------- |
| to initialize an instance | x = MyClass() |x = MyClass()|
| the “official” representation as a string when you do return(x)| repr(x) or x | x.__ repr__()|
| the “informal” value as a string when you do print(x)| str(x) | x.__ str__()|
| the value as a formatted string| format(x, format_spec)|x.__ format__(format_spec)|

---
>> ## Other special Method : Theory and Practical examples
---
In this section, we will see how to use some common magic methods that are important to know in our programming adventure along with python

### Classes That Act Like Iterators
---
#### Theory 
__ iter__() and  __ next__() are called whenever you create a new itertor and retrieve the next value of the iterator. 
In Python, an iterator is an object that can be iterated upon. In simpler words, we can say that Iterators are objects that allow you to traverse through all the elements of a collection and return one element at a time. More specifically, we say that an iterator is an object that implements the iterator protocol.
Iterators are used in both **for loops** and **while loops**. 
![ITER()](img\iter.JPG)

#### Practical Example
Here is a simple example, describing these methods:
 > Example 1 :
``` 
x =[1,2,3,4]
# get an iterator using iter()
a = x.__iter__()
#Get the first item
a.__next__()

#Get the second item
a.__next__()
```
**Output:**

1

2
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
1 2 3 4 5 6 7 8 9 0


### Computed Attributes
---
##### Theory 
Python provides a set of methods that classes can use to access the attributes of an object. Whenever we retrieve or set an object’s attributes, Python calls one of these functions to perform any desired processing. 

__ getattribute__() and __ getattr__(), are called to retrieve an attribute value. These are slightly different from each other. Getattr is called only when the requested attribute can’t be found on the object. Meanwhile, getattribute is called unconditionally every time an attribute name is requested. Additionally, there are __ setattr__, __ delattr__, and __ dir__() to set, delete and discover supported attributes
#### Practical Example
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
    
#==  create an instance of myColor==
cls1 = myColor()
#== print the value of a computed attribute==
print(cls1.rgbcolor)
#(50, 75, 100)
#== same as you are doing like this==
print(cls1._getattribute__('rgbcolor'))
#(50, 75, 100)
#== or doing like this==
getattr(cls1, 'rgbcolor')

print(cls1.hexcolor)
#== set attribute red at 100==
cls1.rgbcolr = [100, 100, 100]
#= same as ==
cls1.__setattr__('rgbcolor', [100, 100, 100]) 

#== delete an attribute==
del cls1.red
#==same as ==
cls1.__delattr__('red')

#== To list all attributes and methods ==
dir(cls1)
#== same as ==
cls1.__dir__()   
```
**Output:**
(50, 75, 100)

The above code modifies the attribute related methods to get colour information. As user passes a supported attribute name, e.g. `rgbcolor` python will return the value corresponding to the name


### Classes That Act Like Functions
---
#### Theory 
It is possible to make an instance of a class callable — exactly like a function is callable — by defining the __ call__() method. 
The __ call__() method enables Python programmers to write classes where the instances behave like functions and can be called like a function. When the instance is called as a function; if this method is defined, x(arg1, arg2, ...) is a shorthand for x.__ call__(arg1, arg2, ...)
#### Practical Example
> Example
```
class Example:
    def __init__(self):
        print("Instance Created")
      
    # Defining __call__ method
    def __call__(self, x):
        return x**2
  
# Instance created
e = Example()
  
# __call__ method will be called
e(2)
```
**Output :**

Instance Created

4
### Classes That Act Like Sets
---
#### Theory 
The following special methods allow us to give our class a container interface, like set. 

Python __ len__() is one of the various magic methods that is basically used to implement the len() function. It finally returns an integer value that is greater than or equal to zero as it represents the length of the object for which it is called. 
| Method | Explanation | Signature |
| ----------- | ----------- |
| The number of items | len(x) invokes x.__ len__ | __ len(self)__|
| To know whether it contains a specific value | x in s | s.__ contains__(x)|

#### Practical Example
> Example 1
```
class GFG:
    def __init__(self, a):
        self.a = a
    def __len__(self):
        return len(self.a)
       
obj = GFG("Kudawoo")
print(len(obj))
```
**Output:**
7
> Example 2

```
import datetime
 
class DateClass(object):
    def __init__(self, startDate, endDate):
        self.startDate = startDate
        self.endDate = endDate
 
    def __contains__(self, item):
        """ check whether a date is between the given range and
        return true or false"""
        return self.startDate <= item <= self.endDate
 
dtObj = DateClass(datetime.date(2019, 1, 1), datetime.date(2021, 12, 31))
result = datetime.date(2020, 6, 4) in dtObj
print("Whether (2020, 6, 4) is within the mentioned date range? ", result)
 
result = datetime.date(2022, 8, 2) in dtObj
print("Whether (2022, 8, 2) is within the mentioned date range? ", result)
```
**Output:**

Whether (2020, 6, 4) is within the mentioned date range?  True

Whether (2022, 8, 2) is within the mentioned date range?  False

### Classes That Act Like Dictionaries
---
#### Theory 
Extending the previous section a bit, you can define classes that not only respond to the “in” operator and the len() function, but they act like full-blown dictionaries, returning values based on keys

|You Want… 	|So You Write… 	|And Python Calls…|
|---------------|------------------------|--------------|
|to get a value by its key |	x[key] 	| x.__getitem__(key)|
|to set a value by its key 	| x[key] = value 	| x.__setitem__(key, value)|
|to delete a key-value pair |	del x[key] |	x.__delitem__(key)|
|to provide a default value for missing keys |	x[nonexistent_key] | x.__missing__(nonexistent_key)|

#### Practical Example
> Example 1
```
class Test(object):
      
    # This function prints the type
    # of the object passed as well 
    # as the object item
    def __getitem__(self, items):
        print (type(items), items)
  
# Driver code
test = Test()
test[5]
test[5:65:5]
test['KUDAWOO']
test[1, 'x', 10.0]
test['a':'z':2]
test[object()]
```
**Output:**

<class 'int'> 5

<class 'slice'> slice(5, 65, 5)

<class 'str'> KUDAWOO

<class 'tuple'> (1, 'x', 10.0)

<class 'slice'> slice('a', 'z', 2)

<class 'object'> <object object at 0x7f75bcd6d0a0>

> Example 2
```
class bank_record:
    def __init__(self, name): 
        self.record = {
                        "name": name,
                        "balance": 100,
                        "transaction":[100]
                        }
    
    def __getitem__(self, key):   
        return self.record[key]
    
    def __setitem__(self, key, newvalue):
          
        if key =="balance" and newvalue != None and newvalue>= 100:
            self.record[key] += newvalue
              
        elif key =="transaction" and newvalue != None:
            self.record[key].append(newvalue)
      
    def getBalance(self):
        return self.__getitem__("balance")
  
    def updateBalance(self, new_balance):
          
        self.__setitem__("balance", new_balance)
        self.__setitem__("transaction", new_balance)    
      
    def getTransactions(self):
        return self.__getitem__("transaction")
  
    def numTransactions(self):
        return len(self.record["transaction"])
  
sam = bank_record("Sam")
print("The balance is : "+str(sam.getBalance()))
  
sam.updateBalance(200)
print("The new balance is : "+str(sam.getBalance()))
print("The no. of transactions are: "+str(sam.numTransactions()))
  
sam.updateBalance(300)
print("The new balance is : "+str(sam.getBalance()))
print("The no. of transactions are: "+str(sam.numTransactions()))
print("The transaction history is: "+ str(sam.getTransactions()))
```
**Output:**

The balance is : 100
The new balance is : 300
The no. of transactions are: 2
The new balance is : 600
The no. of transactions are: 3
The transaction history is: [100, 200, 300]

### Classes That Act Like Numbers
---
#### Theory 
Using the appropriate special methods, you can define your own classes that act like numbers. That is, you can add them, subtract them, and perform other mathematical operations on them.

|You Want… 	|So You Write… 	|And Python Calls…|
|-----------|------------------------|--------------|
|addition |	x + y |	x.__add__(y)|
|subtraction |	x - y |	x.__sub__(y)|
|multiplication |	x * y |	x.__mul__(y)|
|division| 	x / y |	x.__truediv__(y)|
|floor division |	x // y 	|x.__floordiv__(y)|
|modulo (remainder)| 	x % y 	|x.__mod__(y)|
|floor division & modulo| 	divmod(x, y) |	x.__divmod__(y)|
|raise to power |	x ** y |	x.__pow__(y)|
|left bit-shift |	x << y |	x.__lshift__(y)|
|right bit-shift |	x >> y |	x.__rshift__(y)|
|bitwise and 	|x & y 	|x.__and__(y)|
|bitwise xor |	x ^ y |	x.__xor__(y)|
|bitwise or |	x | y 	|x.__or__(y)|

#### Practical Example
> Example 1 
```
class myName:
  
    def __init__(self, nom):
        self.nom = nom
          
    def __add__(self, prenom):
        return myName(self.nom + ' ' + self.prenom)
  
obj1 = myName('KUDAWOO')
obj2 = myName("Sena Kodjovi")
obj3 = obj1 + obj2
print(obj3.nom)
```
**Output:**

KUDAWOO Séna Kodjovi
> Example 2 
```
import numpy as np
     
# make an array with numpy
gfg = np.array([1, 2, 3, 4, 5])
     
# applying ndarray.__pow__() method
print(gfg.__pow__(3))
```
**Output:**

[  1   8  27  64  125]


### Classes That Can Be Compared
----
#### Theory 
If you’re creating your own class and it makes sense to compare your objects to other objects, you can use the following special methods to implement comparisons. 

|You Want… 	|So You Write… 	|And Python Calls…|
|-----------|------------------------|--------------|
|equality |	x == y 	|x.__eq__(y)|
|inequality |	x != y 	|x.__ne__(y)|
|less than |	x < y |	x.__lt__(y)|
|less than or equal to |	x <= y |	x.__le__(y)|
|greater than |	x >  y |	x.__gt__(y)|
|greater than or equal to |	x >= y |	x.__ge__(y)|
|truth value in a boolean contex|t 	if x: |	x.__bool__()|

##### Practical Example
> Example 1
```
class Student:
    def __init__(self, name):
        self.name = name
  
    def __eq__(self, other):
        if isinstance(other, Student):
            if other.name == self.name:
                return True
        return False
  
  
Patrick = Student("Patrick")
David = Student("David")
  
print("David == Patrick : ", (David == Patrick))
```
**Output:**
David == Patrick :  False
> Example 2
```
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __bool__(self):
        if self.age < 18 or self.age > 65:
            return False
        return True


if __name__ == '__main__':
    person = Person('David', 16)
    print(bool(person)) 
---
**Output:**
False

```
**Output:**
David == Patrick :  False

---
## Use cases in data analysis
---

## Conclusion 
---
It is a must konw to understand special mmethod to manipule objects, series, dataframe or multiframe in python ans to process data. 
Understanding what is under the hood will facilitate manipulation of objects of class among them
