---
layout: post
title:      "ME, MYSELF AND ‘SELF’ "
date:       2018-04-18 18:26:39 -0400
permalink:  me_myself_and_self
---

I thought I understood the concept of ‘self’ in Ruby, until I had to verbally explain its use and I realised my understanding of this abstract idea was a little blurry. 

I decided to do some extra reading so I could understand fully how and why it is used. 

so…….I understand the keyword ‘Self’ always refers to an object. What the object is, depends on the context that ‘Self’ is used in.

In class methods, the ‘self’ keyword refers to the class itself.
 
for example : 

class Student
  def self.about
    self
  end
end
 
Student.about  ( calling the about method on the Student class )

We can see that ‘self’ is used explicitly before the class method and dot operator to define a class method.

In instance methods, the  ‘self’ keyword is used inside the method, and refers to instances of the class.

For example: 

class Student
  def address
    self
  end
end
 
Student.new.address  (an instance of the Student class)

In the example above, the keyword ‘self’ refers to the current object - the instance of the Student class 

Where else might I see the word ‘Self’? 

‘Self’ can also refer to modules and the ‘top-level’ namespace of the program - the main object. 

What happens if I forget to explicitly put ‘self’ when we call a method? 

Apparently this is no problem! When we don’t specify a receiver, the implicit self is used which is the value of the ‘self’ keyword. The receiver defaults to the current object, ‘self’.

hmm…I found myself asking “when do I actually need to use ‘self’”? 

I have to use ‘self’ when defining a class method, otherwise Ruby will automatically assume that I am creating an instance method.  

Secondly, I could also use ‘self’ to avoid ambiguation within a method. Sometimes
Ruby needs help distinguishing between method calls and local variables or local variable assignment.

For example, what happens when we don’t use the symbol ‘@‘? : 

class Dog
  attr_accessor :name

  def replace_name(new_name)
    name = new_name
  end

  def print_name
    puts name
  end
end

doggy = Dog.new
doggy.name = "Bonnie"
doggy.replace_name("Clyde")
doggy.print_name
# “Bonnie"

I would have  expected to see ‘Clyde’ as the result of running the print_name method, so why did the dog’s name stay as ‘Bonnie’? If we look closer at the replace_name method we can see that ‘name = ‘ is being treated as variable assignment by Ruby, and NOT as the setter method “name=“. We can change this by simply adding ‘self’ in front of ‘name’  like this :


def replace_name(new_name)
    self.name = new_name
  end

Now Ruby knows that we are not trying to set a local variable, we are calling a method on the instance of the object. 

I’d like to think I am a bit more ‘self’ aware now ( sorry, I had to get that in somewhere) 

I found the following websites particularly helpful on this topic:

https://www.jimmycuadra.com/posts/self-in-ruby/
https://codequizzes.wordpress.com/2014/04/07/rubys-self-keyword-and-implicit-self/
https://hackhands.com/three-golden-rules-understand-self-ruby/
