# Chapter 9
# Exception Handling
* As name says exception handling is used for handling exceptions.
* Exceptions is triggered before the execution 
* So even if there is an error or not exception will be executed.

### Basic Syntax
```
begin
    "Include the statements , conditions.."
rescue
    "The alert to be displayed"
end
```

### Basic Example
* If we try to create instance for Module => It should display an alert

```
puts "Lets start"

module Wish
    def hello
        "You cant reach me now"
    end
end

begin
    wish = Wish.new
rescue
   p  "Instance cannot be created for Module"
end

p "Stop"    
        
```

## How to find the execption messages and class?
```
def method_1
    p "started method 1"
    begin
    	method_2
	rescue => e
	    p "caught exception"
	    p "error class: #{e.class}"
	    p "error message: #{e.message}"
	    p "backtrace : #{e.backtrace}"
	end

	p "Stopped method 1"
end

def method_2
    p "started method 2"
    begin
	method_3
    end
    p "stopped method 2"
end

def method_3
    p "started method 3"
    begin
	    # 1/0
	    "abc".hello
	# rescue
	# p "caught by exception 3"
    end
	p "stopped method 3"
end

method_1

OUTPUT:
"started method 1"
"started method 2"
"started method 3"
"caught exception"
"error class: NoMethodError"
"error message: undefined method `hello' for \"abc\":String"
"backtrace : [\"lib/exception2.rb:27:in `method_3'\", \"lib/exception2.rb:18:in `method_2'\", \"lib/exception2.rb:4:in `method_1'\", \"lib/exception2.rb:34:in `<main>'\"]"
"Stopped method 1
```


### raise
* Used to raise an error when condition is not satisfied
> Method 1  (RuntimeError)
```
def currency(country)
	case country
	when :japan
		'yen'
	when :vietnam
		'dong'
	when :india
		'rupee'
	else
		raise "I am not sure about the currency of #{country}"
	end
end

p currency(:germany)    => I am not sure about the currency of germany (RuntimeError)
```
> Method 2 (Argument Error)
```
def currency(country)
	case country
	when :japan
		'yen'
	when :vietnam
		'dong'
	when :india
		'rupee'
	else
		raise ArgumentError, "I am not sure about the currency of #{country}"
	end
end

OUTPUT:
=>  I am not sure about the currency of germany (ArgumentError)
```
### Exception Handling for regular expression
> Method 1: Normal method
```
def regular_expression
	begin
		print "Text?:" 
		text =  gets.chomp
		print "Pattern?:" 
		pattern = gets.chomp
		regexp = Regexp.new(pattern)
		matches = text.scan(regexp)
		matches.size >0 
		p  "Pattern Matched #{matches.join(', ')}"

	rescue
		p "Invalid pattern format"
	end
end

regular_expression

```

>Method 2: RegexpError
```
def regular_expression
	begin
		print "Text?:" 
		text =  gets.chomp
		print "Pattern?:" 
		pattern = gets.chomp
		regexp = Regexp.new(pattern)
		matches = text.scan(regexp)
		matches.size >0 
		p  "Pattern Matched #{matches.join(', ')}"

	rescue RegexpError => e
		p "class : #{e.class}"
		p "message: #{e.message}"
	end
end

regular_expression


OUTPUT:
    Text?:123-456-789
    Pattern?:[1-6+
    
    "class : RegexpError"
    "message: premature end of char-class: /[1-6+/"
    
VALID OUTPUT:
    Text?:123-456-789
    Pattern?:[1-6]+
    
    "Pattern Matched 123, 456"
```

### ensure

```
def check_type
	print "Enter the number:"
	number = gets.to_i

	begin
		number %2 == 0
		'OK'
	rescue
		"Oops the number is   not odd"
	ensure
	 return "done"
	end
end

p check_type    => "done"
```

### rescue
* Consider fizzbuzz problem
```
    def fizzbuzz(number)
        if number %3 ==0 && number%15 !=0
            "fizz"
        
        elsif number %5 ==0 && number%15 !=0
            "buzz"
        
        elsif number % 15 ==0
            "fizzbuzz"
        else
            number.to_s
        end
        rescue => e
            p "#{e.class} #{e.message}"
            raise
    end
    fizz_buzz(nil)    => "error message and class"        
            
```