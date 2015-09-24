# Instance Variables

## Objectives

1. Define instance variables.
2. Understand why we need to use them and how they work.

## What Is An Instance Variable?

We've been working with variables for a while now. For example:

```ruby
bro_greeting = "Sup, bro?"
```

The code above sets a variable, `bro_greeting`, equal to the string `"Sup, bro?"`. Now, we can use that variable to read and operate on that string.

```ruby
bro_greeting
  => "Sup, bro?"

bro_greeting.upcase
  => "SUP, BRO?"
```

The `bro_greeting` variable is what's known as a **local variable**, so named because it can only be accessed in a specific, local environment.

A local variable that is defined inside one method, for example, cannot be accessed inside another. In order to get around this limitation, we can use **instance variables** inside our Ruby classes.

An **instance variable** is a variable that is accessible in any instance method.

## We Need Instance Variables

**If you want to code along with this reading, put this project on your computer and open in Sublime text.**

Let's say we have a class called `Dog` that is responsible for producing individual dog objects. We want each dog to be able to have a name and show it's name. So, we need to write some methods:

```ruby
class Dog
	def name=(dog_name)
		this_dogs_name = dog_name
	end

	def name
		this_dogs_name
	end
end
```

Here we define two instance methods, the `name=`, or "name equals" method, and the `name` method. The first method takes in an argument of a dog's name and sets that argument equal to a variable, `this_dogs_name`. The second method is responsible for reporting, or reading the name.

Here's how it **should** work in practice:

```ruby
lassie = Dog.new
lassie.name = "Lassie"

lassie.name
	=> "Lassie"
```

Our two methods are responsible for "setting" and "getting" an individual dog's name.

Open up the `dog.rb` file in this repository and you should see our `Dog` class defined, as well as the above code to create a new dog instance, give it a name and try to access, or read, it's name.

Run the file in your terminal by typing `ruby dog.rb`. You should see the following error:

```
dog.rb:8:in `name': undefined local variable or method `this_dogs_name' for #<Dog:0x007ffd609ed0a8> (NameError)
	from dog.rb:15:in `<main>'
```

Uh-oh. Looks like the `#name` method doesn't know about the `this_dogs_name` variable from the `#name=` method. That is because `this_dogs_name` is a **local variable**. A local variable has a **local scope**. That means that it cannot be accessed outside of the method in which it is defined.

## Implementing Instance Variables

An instance variable is defined by prefacing the variable name with a `@` symbol.

Instance Variables are bound to an instance of a class. That means that the value held by an instance variable is specific to whatever instance of the class it happens to belong to. Instance variables hold information about an instance, usually an attribute of that instance, and can be called on throughout the class, without needing to be passed into other methods as arguments (as would be the case with local variables).

Let's refactor our `Dog` class to use an instance variable instead of a local variable to set and get an individual dog's name.

Open up `dog.rb` and change the `Dog` class in the following way:

```ruby
class Dog

  def name=(dogs_name)
    @this_dogs_name = dogs_name
  end

  def name
    @this_dogs_name
  end
end

lassie = Dog.new
lassie.name = "Lassie"

puts lassie.name

```

Run the file again by typing `ruby dog.rb` in your terminal and you should see `Lassie` outputted to your terminal.


It worked! Why did it work? Inside the `#name=` method, we set the value of `@this_dogs_name` equal to whatever string is passed in as an argument. Then, we are able to call on that same instance variable in a totally separate method, the `#name` method.

## Conclusion

As we dive deeper into object oriented Ruby, we'll be using instance variables frequently to pass information around the instance methods of a class. Think of instance variables as the containers for instance-specific information. The ability of instance variables to store information and be accessible within different instance methods is one of the things that makes it possible for us to create similar, but unique objects in object orientated Ruby.
