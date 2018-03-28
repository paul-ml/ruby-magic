# chapter 8
# Modules

## deep_freeze
* Let us ASSUME that we have an ARRAY with the countries
```
    countries = ["Japan", "Vietnam", "China", "India"]
```
* data inside the array is not safe - ANYONE CAN UPDATE IT
```
   countries[0].upcase    => "JAPAN"
```
* It can be restricted by using the following code:
```
    countries = ["Japan".freeze,"Vietnam".freeze,"China".freeze, "India".freeze].freeze
```
* But practially for a LARGE DATASET it is NOT EASY
* So, deep_freeze was introduced.
```
class Country
    COUNTRIES = deep_freeze(["Japan","Vietnam","China","India"])
end

    Country::COUNTRIES.frozen?    => true
    Country::COUNTRIES.all?{|country| country.frozen?}    => true
```


### Modules
* Modules are similar to class and declaration of modules is also same as class
* But following operation cannot be performed:
- [x]     Instance cannot be created
- [x] cannot be inherited
```
   1.   module Hello
        end
        hey = Hello.new     => NOT POSSIBLE
        
   2. module Hey < Hello    => NOT POSSIBLE
```
### Difference between extend and include
> Extend
* Instance variable (object) of class cannot access a module method 
```
## NOT POSSIBLE ##

    module Loggable
	def log(text)
	    p text
	end
    end

    class User
	extend Loggable

	def logged
	    log("hey buddy")
	end
    end

    user = User.new
    user.logged        =>ERROR
```
* By using extend, class can access Module method
```
module Loggable
    def log(text)
	p text
    end
end

class User
    
    extend Loggable

    log("hey buddy")
end
                => "hey buddy"

OR

class User
    extend Loggable

    def self.logged
	log("hey buddy")
    end
end

User.logged    => "hey buddy"
```

> Include
* Enables the class object to access a method in module
```
    module Loggable
        def log(text)
	    p text
	end
    end

    class User 
	include Loggable

        # log("hey buddy") => error

        def logged_in
	    log("User logged in")
        end
    end

    user = User.new
    user.logged_in
```

* But class cannot access method in module directly
```
    module Loggable
        def log(text)
	    p text
	end
    end

    class User 
	include Loggable

        log("hey buddy")    => ERROR/NOT POSSIBLE
    end    
        
```

> extend and include
* If we use include and extend method : both class and class objects can access module 
```
    module Loggable

	def log(message)
	    p message
	end    
    end

    class User
        include Loggable
        extend Loggable
	    
        log("hey buddy")    => "hey buddy"
	
        def logged
	    log("tada")  => "tada"
        end
    end

    user = User.new
    user.logged
```
### To find the included modules
* To find the included modules , following methods can be used :
* class_name.include?()
* class_name.included_modules
* class_name.ancestors
```
module Loggable
    def log(text)
	p text
    end
end

class User 
    include Loggable

    # log("hey buddy") => error

    def logged_in
	log("User logged in")
    end
end

user = User.new
user.logged_in    => "hey buddy"

p User.include?(Loggable)    => true
p User.included_modules      => [Loggable, Kernel]
p User.ancestors             => [User, Loggable, Object, Kernel, BasicObject]

```
> Comparable
```
<=> : gives either +1 0 -1 as output
     
     5 <=> 1     => 1
     2 <=> 2     => 0
     1 <=> 2     => -1
     2 <=> 'abc' => nil
     
     'abc' > 'def'    => false
     'abc' <= 'abd'   => true
     'abc' == 'abc'   => true 
     
     
```

> kernal
```
puts p print require loop    (comes under  kernal)
```

> Structure
*  Level 1: =>  [Basic object , Kernal]
*  Level 2: => [Object]
*  Level 3: => [Module]
*  level 4: => [class]

### Extend without a class

```
    module Loggable
        
        def update_log(message)
            "[LOG] #{message}"
        end
    end
    
    s= 'abc'
    s.update_log(message)    => ERROR
    
    s.extend(Loggable)
    s.update_log("Log updated")    => "Log updated"
```

### Class within a module
> when 2 class are having the same name but different methods
```
module Basketball
    class Second 
	def initialize(name, number)
	    @name = name
	    @number = number
        end
    end
end

module Clock
    class Second
	def initialize(second)
	    @second = second
	end
    end
end


p Basketball::Second.new("Paul", 44)
p Clock::Second.new(100)
```

### Module function
* syntax: module_function :method_name
* module_function is used to make a method in module private

* Lets consider a normal example using module
```
module Loggable

	def update_log(message)
		"[LOG] #{message}"
	end
	# module_function :update_log
end

class User

    include Loggable 
end

user = User.new
p user.update_log("Logged in")    => "[LOG] Logged in"
```

* Now lets consider an example with module_function
```
module Loggable

    def update_log(message)
	"[LOG] #{message}"
    end
    module_function :update_log
end

class User

    include Loggable 

end

user = User.new
p user.update_log("Hello")    => private method `update_log' called for #<User:

```

### Module Math
1. Math::E => 2.718281828459045 (Eulers value)
2. Math::PI => 3.141592653589793
3. Math.sqrt(2) => 1.4142135623730951

In class module math can be added in the same way as adding normal modules : include Math


### singleton
* Each newly created instance will have the same configuration.
```
require 'singleton'

class Configuration

	include Singleton

	attr_accessor :base_url, :debug_mode

	def initialize 
		@base_url = ''
		@debug_mode = false
	end

end

# config = Configuration.new  => private method `new' called for Configuration:Class

config = Configuration.instance

p config.base_url = 'https://wwww.pjdesignz.com'
config.debug_mode = true


config2 = Configuration.instance

p config2.base_url    => 'https://wwww.pjdesignz.com'
p config2.debug_mode  => true
p config2.debug_mode.equal?(config.debug_mode)     => true

config2.debug_mode = false    

config3 = Configuration.instance
p config3.debug_mode  => false

p config.debug_mode   => false
``` 

### Superclass
* superclass is the parent class
```
module A
    def to_s
        "<A> #{super}"
    end
end

module B
    def to_s
	"<B> #{super}"
    end
end

class Product

    def to_s
	"<Product> #{super}"
    end
end

class Ipod < Product

    include A
    include B

    def to_s
        "<Ipod> #{super}"
    end
end

ipod = Ipod.new
p ipod.to_s    => "<Ipod> <B> <A> <Product> #<Ipod:0x007fce898ccfa8>"

ipod.ancestors    => [Ipod, B, A, Product, Object, Kernel, BasicObject]
```

### inlcude with modules and class
* works  like a chain ..
```
module Ipod
    def ipod_model
	"iPod nano"
    end
end

module Ipad
    include Ipod

    def ipad_model 
	"Ipad Mini"
    end
end

class Apple
    include Ipad
end

apple = Apple.new
p apple.ipod_model, apple.ipad_model

```

### Prepend in module
* As already mentioned prepend is used for attaching the values in beginning
```
module A
    def to_s
	"<A> #{super}"
    end
end

class Sample
    prepend A
    def to_s
	"<Sample> #{super}"
    end
end

sample = Sample.new
p sample.to_s    => "<Sample> <A> #<Sample:0x007fdd7023c0f8>"
```

### Refinements
```

```


## Doubts
1. Singleton
2.  8.9.5 refinements
