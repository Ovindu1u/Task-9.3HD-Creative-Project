# Hash Maps

Hash maps, also known as associative arrays or dictionaries, provide a powerful mechanism for storing and retrieving data efficiently. They are essential data structures with a wide range of applications in software development.

In this tutorial, we will explore hash maps in C++ and discover how they can simplify your programming tasks. We'll cover topics like implementation details, key operations, and practical examples to demonstrate their usage.

The main difference between an array and a hashmap is the way you refference a value in them. While we use an index in the case of arrays, we use **Keys** in hashmaps.

This means that hashmaps do store there **values** unordered, so you will have to keep this in mind that not all aplications might be compatible with hash maps.

A hashmap stores there values in whats known as a **key pair**. Which associates a **key** to a **value**, for example:

```
{"Key", value}
{"Banana", 6}
{"Apple", 12}
```





## Implementing Hash Maps in C++
---

In C++, there are two types of hashmaps that come with the C++ standard library, **maps** and **unordered maps**.

The main difference between the two is that **maps** store there values in the order of the keys, while **unordered maps** do not. For this example we will be using **maps**.


To get started, lets include the header files and namespaces required:

```cpp
#include <iostream>
#include <map>

using namespace std;
```

**iostream** is for basic input output operations and **map** is the hashmaps.
We will be using the namespace std, to avoid writing `std::` every time we use a method from the standard library (like map). 

### Declaring a Hash Map:
<span></span>

```cpp
//format:
map<key_type, value_type> map_name;

//example:
map<char, int> my_map;
```

So lets break it down. Here we are declaring a variable of type **map** with a template (the <> defines a template) of <span style="color:dodgerblue">char</span> and <span style="color:dodgerblue">int</span> followed by the variable name **my_map**. Note that the key and value types can be any type, even custom types created by you.

### Key Pairs
#

As we mentioned earlier, an hashmap is a set of **key pairs** so we need to know to decalre them as well, there are two main ways:

```cpp
//using a pair object:
pair<char, int> kp('A', 5);

//or using an initializer list:
{'A', 5};
```

both methods perfrom the same function with a few exceptions, as you can see using an initializer list is much simpler, and we will be using that.

## Using Hashmaps in C++
___

One way of assigning keypairs to a map, especially at declaration is:

```cpp
my_map =     
    {
        {'A', 10},
        {'Z', 20},
        {'C', 30},
        {'L', 40}
    };
```

Here we are setting **my_map** to set of key-pairs. It is important to note that doing this will **replace** the hashmap instead of **inserting** to it.   
Here are two ways of inserting to an hashmap:

### Element Modification


```cpp
my_map['K'] = 17;
```
This is a common way of inserting / modifying entries in a hashmap, in this case if the key already exists in the hashmap, we will assign it to the given value, if the key does not exist, this will insert a new keypair to the hashmap.

### Using the Insert function

```cpp
my_map.insert({'O', 10});
```

In this method, we are making use of the function insert in the map class. This function will takes a **pair**  as the argument and inserts it to the hashmap, however if the **key** already exists in the hashmap, the function will not modify the existing keypair, unlike the **Element Modification** method.

### Getting a value in an Hashmap
<span></span>

```cpp
    cout << my_map['A'] << endl;
```
This code will print out the value associated with the key **'A'**. However if the key does not exist, we will get 0 as the value. But we cannot determine if the key did not exist or if the key was associated with the value 0, this is when we use the `find()` method. 

### Finding a value in a Hashmap

The `find()` method returns an "**Iterator"** pointing to the element with the specified key if found, else it will return `map.end()` which is the Iterator pointing to position right after the last element in the map. To demonstrate this, we will create a function called `key_exists` that will return <span style="color:dodgerblue">true</span> if the value exists.

```cpp
bool key_exists(map<char, int> &hashmap, char key)
{
    auto iter = hashmap.find(key);

    if (iter == hashmap.end())
    {
        return false;
    }
    else
    {
        return true;
    }
}
```

```cpp
int main()
{
    map<char, int> my_map =     
    {
        {'A', 10},
        {'Z', 20},
        {'C', 30},
        {'L', 40}
    };

    if(key_exists(my_map, 'P'))
    {
        cout << "Key Exists" << endl;
    }
    else
    {
        cout << "Key does not Exist" << endl;
    }
}
```
```
output:

Key does not Exist
```

Let's break it down. The key exist functions takes a map object with template <<span style = "color:dodgerblue">char</span>, <span style= "color:dodgerblue">int</span>> and the key to find. the <span style = "color:dodgerblue">auto</span> keyword is a way of telling the C++ compiler to automaticaly set the type of **iter** to the type of what `find()` returns. Then we check if the **iter** is equal to `end()`, if it does, it means that the key does not exist, so we return false, else we return true.


## Iteration of Hashmaps in C++
---

We use a similar method to Finding a key in a hashmap when iterating through a hashmap, with the use of pointers. To demonstrate this, we will create a function called `print_hashmap()` that will print out all the keys and associated values.

```cpp
void print_hashmap(map<char, int> &hashmap)
{   
    for(auto iter = hashmap.begin(); iter != hashmap.end(); iter++)
    {
        cout << iter->first << " : " << iter->second << endl;
    }
}
```

```cpp
int main()
{
map<char, int> my_map =     
{
    {'A', 10},
    {'Z', 20},
    {'C', 30},
    {'L', 40}
};

print_hashmap(my_map);
}   
```
```
output:

A : 10
C : 30
L : 40
Z : 20
```

Lets break it down. Just like previously, the function accepts a hashmap object with the same template.
In the for loop, just like before we use the keyword <span style = "color:dodgerblue">auto</span> to assign **iter** to the iterator object of `begin()`, which is the first element in the hashmap, then we increment **iter** while **iter** is not equal to the iterator of `end()`, which is the position right after the last element. 

Then when we print out the keys and values, we use `->`, this is because iter is just a pointer pointing to a keypair. Using the arrow we can access the value in **first** and **second**, which correspond to key and value.

# Conclusion

In conclusion, hash maps, also known as associative arrays or dictionaries, are powerful data structures in C++ for efficiently storing and retrieving key-value pairs. They provide a way to access values using keys instead of indices like in arrays.

In C++, hash maps can be implemented using the `map` class from the C++ standard library. There is also an `unordered_map` class available, which does not maintain the order of the keys.

To use hash maps, you need to include the **<map\>** header file and declare a map object with the desired key and value types. You can assign values to the map using element modification or the `insert()` function.

To retrieve a value from a hash map, you can use the key as an index, similar to arrays. However, if the key does not exist, it will return a default value, which can lead to ambiguity. In such cases, you can use the `find()` method, which returns an iterator pointing to the element if found or `map.end()` if not found.

You can iterate over a hash map using a `for` loop and an iterator. The iterator allows you to access the key-value pairs using the `->` operator, where **iter->first** represents the key and **iter->second** represents the value.

Overall, hash maps provide a convenient and efficient way to work with key-value data in C++. They are widely used in various applications to store, retrieve, and manipulate data based on keys.

## Created by

Ovindu Undugoda
