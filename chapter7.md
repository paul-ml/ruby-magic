# Chapter 7
# Class

### Custom Class
* In ruby we can create custom classes
* Following is a program to display full name of user
```
    class User
	attr_accessor :first_name, :last_name

	def initialize(fname,lname)
		@first_name = fname
		@last_name = lname
	end

	def full_name
		"#{@first_name} #{@last_name}"
	end
end
#Insert in Array format
users = []
users << User.new('Paul Joe', 'George')
p users << User.new('Jowin', 'George')

# Without inserting into array
p jose = User.new('Jose', 'Joseph')
p "full name of Jose is  #{jose.full_name}"

# Access user details from aray
p users[0]
p users[0].first_name
p users.last.first_name

# Call a class method
users.each do  |user|
	p user.full_name
end

# Access values using class object
users.each do |user|
	"#{user.first_name} #{user.last_name}"
end
```
### Multiple class with same name
* Program to print Hello and Bye belonging to 2 different class with same name
```
    class Wish
        def hello
	    "hello"
        end
    end

    class Wish
        def bye
	    "Bye"
        end
    end

    wish = Wish.new
    p wish.hello    => "Hello"
    p wish.bye      => "Bye"
```

> What is self.method in Class
* By using self a method can be called directly by using class_name. 
* Following program will help to understand it quickly
```
    Case 1:(without self method)

        class User 
	    def hello
	        "hello"
	    end
        end

        p user = User.hello    =>ndefined method `hello' for User:Class (NoMethodError)

    Case 2: (With self method)
        
        class User
            def self.hello
                "Hello"
            end
        end
        p user = User.hello    => "hello"
```
> GLOBAL VARIABLES
* Program using global variables self.methods and normal class methods
```
    class Product
	$default_price = 0
	def self.price
		$default_price
	end
	def price
		$default_price  = $default_price + 10	  #Now default value is replaced by 10
	end
	def outstanding_price
		$default_price		# 10
	end
    end

    p Product.price

    product = Product.new
    p product.price

    p product.outstanding_price
        
```

### Self keyword
* Lets see a program to have complete idea about keyword self
```
class User
	attr_accessor :name

	def initialize(name)
		@name = name
	end

	def change_name_to_bob
		name = 'Bob'
	end

	def change_name_to_jacob
		self.name = 'Jacob'
	end

	def change_name_to_antony
		@name = 'Antony'
	end
end

p user = User.new('Paul')
user.change_name_to_bob    => Bob
p "name_changed to: #{user.name}" =>Paul

user.change_name_to_jacob    => Jacob
p "name changed to: #{user.name}"    => Jacob

user.change_name_to_antony    => Antony
p "name changed to: #{user.name}"    => Antony
```
* if we check the method change_name_to_bob , local variable name is replaced by "Bob" but this cannot reflect to actual users name
* Inorder to replace actual users name either keyword self.name or "@name" has to be replaced 

> self method with a self method:
```
Case 1 :
        class Sample
	    def self.foo
	        p "hello I am redirecting to bar"
	        bar    # or self.bar
	    end

	    def self.bar
		p "yes i am bar"
	    end
        end
        Sample.foo    => "hello I am redirecting to bar"
                      => "yes i am bar

Case2 :(trying to call a normal method from self.method)
        
        class Sample
	    def self.foo
	        p "hello I am redirecting to bar"
	        bar
	    end

	    def bar
		p "yes i am bar"
	    end
        end
        Sample.foo    => NOT POSSIBLE
    
Case 3:
        sample = Sample.new
        sample.bar => "yes i am bar"
```
> How to call a self method from a normal method?
```
    class Sample
        def self.foo
            p "hello i am redirecting to bar"
        end
        def bar 
            Sample.foo    #classname.method_name
             "yes i am bar"
        end
    end
    sample = Sample.new
    p sample.bar    => "hello I am redirecting to bar"
                    => "yes i am bar"
    
        
```


### Inheritence
* It is the ability of one class to inherit properties from parent class.
* Syntax: child_class < parent_class
> Keywords
```
    class User
    end
    user = User.new
    user.class => User
```
> instance_of?
```
Example:
    user.instance_of?(User)    => true
    user.instance_of?(String)  => false
    user.instance_of?(Object)  => false
```
> is_a?
```
Example:
    user.is_a?(User)    => true
    user.is_a?(Object)  => true
    user.is_a?(class)   => false
    user.is_a?(String)  => false
    User.is_a?(Class)   => true
```
> Method 1:
```
# PARENT CLASS
    class Product
        attr_accessor :name , :price

        def initialize(p_name, price)
            @name = p_name
            @price = price
        end

        def details
            "product: #{name} price: #{price}"
        end
    end

#INHERITED CLASS
    class Ipod < Product
    end
    
    ipod = Ipod.new("Ipod", 10000)
    p ipod.details  

Output: 
"product: Ipod price: 10000"
```
> Method 2
* When inherited class is accessing the attributes of parent class along with its own attribute
```
class Product
    attr_accessor :name , :price

    def initialize(p_name, price)
	@name = p_name
        @price = price
    end

    def details
    	"product:name #{name} product price: #{price}"
    end
end

class Ipod < Product
    attr_accessor :colour

    def initialize(name,price,colour)
    	super(name,price)
    	@colour = colour
    end

    def breif_idea
    	"product: #{name} price: #{price} colour: #{colour}"
    end
end

ipod1 = Ipod.new("iPod Nano", 10000,"orange")
p ipod1.breif_idea

```
>  self keyword within inherited class
```
Case 1: (when public)
# Parent class
class Parent
    def self.hello
        "hello"
    end
end

# Child class
def Child < Parent
end

Output:
Child.hello     => "hello"
Parent.hello    => "hello"
    
    
case2: (when private)

# Parent class
class Parent
    private
    def self.hello
        "hello"
    end
end

# Child class
def Child < Parent
end

OUTPUT: 
Child.hello     => "hello"
Parent.hello    => "hello"

case 3: 
when self keyword is removed and if hello is a private method? => ERROR
```

### Gloabal Variables and Class tricks

> ::
```
    class Product
        DEFAULT_PRICE =0
    end
    Product::DEFAULT_PRICE     => 0
        
```
* if class is freezed
```
    class Product
        Product.freeze
        DEFAULT_PRICE =0
    end
    Product::DEFAULT_PRICE     =>can't modify frozen #<Class:Product>
```
> Access global arrays and hash
```
    class Product
        NAME = "iPhone"
        MODELS = ["4s","5s","6s","7s"]
        PRICE = {"4s" => 10000, "5s" => 20000, "6s" => 30000, "7s" => 40000}
        
        def remove_fourS
            Product::Models.delete("4s")
            Product::Models
        end
    end
    
    Product::NAME => "iPhone"
    p Product::MODELS    => ["4s", "5s", "6s", "7s"]
    p Product::PRICE     => {"4s"=>10000, "5s"=>20000, "6s"=>30000, "7s"=>40000}
    p Product::MODELS[0] => "4s"   
    p Product::PRICE["5s"] => 20000
    
    product = Product.new
    product.remove_fourS    => ["5s","6s","7s"]
        
```
>  When global array is freezed operations like deletion cannot be performed

```
    MODELS = ["4s","5s","6s","7s"].freeze
    
Now , if we call remove_fourS method following error message will be displayed: 
   => `delete': can't modify frozen Array
```

> It is possible to upcase a freezed global_array values
```
    class Fruit 
        NAMES = ["apple", "orange", "grape"].freeze
    end
    Fruit::NAMES[0].upcase     => "APPLE"
```
> To make the previous condition false
```
     class Fruit 
        NAMES = ["apple".freeze, "orange".freeze, "grape".freeze].freeze
    end
    Fruit::NAMES.delete("apple")     => Freezed alert
```

### Instance variable
```
    class Product
	@name = 'Product'

	def self.name
		@name    //@name = 'Product'
	end

	def initialize(name)    //Initialized as 'Sample product'
		@name = name
	end

	def name
		@name    //Initialized value
	end
end

p "Product.name is:" +  Product.name

product = Product.new('Sample product')
p product.name


```
### Class variable
* Begins with @@ ->  Example: @@name
* Class variable is shared among all objects of a class
* only one copy of class variable is available
```
    class Product
	@@name = "iPhone"

	def self.name
		@@name
	end

	def initialize(name)
		@@name = name
	end

	def name 
		@@name
	end

	def upcase
		@@name.upcase
	end
end


class Ipod < Product
	@@name = 'Ipod'

	def self.name
		@@name
	end

	def initialize(name)
		@@name = name
	end

	def name
		@@name
	end

	def upcase
		@@name.upcase
	end
end

# Lets check the output now

p Product.name  # => Ipod ------> As instance variable @@name is replaced by iPod
p Ipod.name     # => Ipod

product = Product.new('iPad')

p product.name			# => iPad		
p product.upcase		# => IPAD

p Product.name			# => iPad

ipod = Ipod.new('ipod Nano')

p ipod.name		# => "ipod Nano"
p ipod.upcase		# => "IPOD NANO"
p product.name		# => "ipod Nano"
p product.upcase	# => "IPOD NANO"
p Product.name		# => "ipod Nano"
p Ipod.name		# => "ipod Nano"

```
### Global Variables
```
$name = 'Paul Joe George'

class User

	def initialize(name)
		$name = name
	end

	def self.name
		$name
	end

	def name
		$name
	end

end

# Lets check the output now

p User.name	        # => "Paul Joe George"

user  = User.new('Jowin George')	

p user.name		# => "Jowin George"
p User.name		# => "Jowin George"


```

### Ruby Specifications and class definition

> alias
* To call the same method in different names
```
class Hello
	
    def hello
    	"its a greeting"
    end

    alias greeting hello
end

konnichiwa = Hello.new

p konnichiwa.hello     => "its a greeting"
p konnichiwa.greeting  => "its a greeting"
```

> Nested class
* Class within a class
```
class Human
    class Student
	def initialize(value)
	    @age = value
        end
        def age
	    @age
	end
    end
end

student = Human::Student.new('20')
p student.age    => 20

```
### Operations with class
```
class Product
    attr_accessor :name, :code

    def initialize(name, code)
	    @name = name
	    @code = code
    end	
end

product1 = Product.new("ipod1",101)
product2 = Product.new("ipod Nano", 102)
product3 = Product.new("ipod2", 101)

p product1.code == product2.code    => false
p product2.code == product3.code    => false
p product1.code == product3.code    => true

```
> Method in the form of comparison operator
```
class Product
    attr_accessor :name, :code

    def initialize(name, code)
    	@name = name
    	@code = code
    end
    def ==(other)    # Its working like a normal method (say : def hello(other))
    	if other.is_a?(Product)
    		code == other.code 
    	else
	    false	
	end
    end

end

product1 = Product.new("ipod1",101)
product2 = Product.new("ipod Nano", 102)
product3 = Product.new("ipod2", 101)

p product1.code == product2.code    => false
p product2.code == product3.code    => false
p product1.code == product3.code    => true

p product1. ==(product3) => true
p product1.==(1)         => false    # method call is also in the same format

```

### Inbuild class
> Example : String
```
class Hello < String
end

p hello = Hello.new('Hello')    => "Hello"
```
> Array
```
class Name < Array
end

names = Name.new()
names << 1
names << 2
p names    => [1,2]
```

### When same class is defined twice
* when same class is defined twice, new data will be added to the existing class definitions and old data will be updated by new values.
```
class User
    attr_accessor :name, :age
	
    def initialize(name, age)
    	@name = name
    	@age = age
    end

    def status
    	"This is #{@name} and I am a student"
    end

end

user = User.new("Paul Joe George", 22)
p user.status


# later after my graduation I changed my status from student to employee
#defining the same class again

class User
	
    alias new_status status

    def status
	"This is #{@name} and I am  an employee "
    end

# And I added a new method after a long time

    def location
	"Moved from India to Japan"
    end
end


p user.new_status	 # => "This is Paul Joe George and I am a student"
p user.status           # => "This is Paul Joe George and I am  an employee "
p user.location	 # => "Moved from India to Japan"
p user.status           # => "This is Paul Joe George and I am  an employee "


```


* > Alternate methods:
```
    class Name
        def self.hello
            "hi"
        end
    end
    
    -- SAME AS --
    
    class Name
        class << self
            def hello
                "hi"
            end
        end
    end
                
```
