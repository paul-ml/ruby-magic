# Chapter 10

# Yield

## Basic example for yield
```
def sum
	a=5
	yield
	p "Sum is #{a + yield}"
end

sum do
	b = 25	# This value will go to the place from where yield is called.
end

OUTPUT: 
=> "Sum is 30"
```
> Access above  method: sum
```
sum => `sum': no block given (yield) (LocalJumpError)
```
> How to resolve the LocalJumpError?
* block_given? -> can be used
```
def sum
	a=5
	if block_given?
		yield
		p "Sum is #{a + yield}"
	else
		p "first number is #{a} but second number is missing"
	end
end

sum     => "first number is 5 but second number is missing"
```

> Passing value with yield
* Case 1
```
def square 
	print "Enter the number:"
	number = gets.to_i

	number = yield(number)
end

square do |number|
	p number * number	
end

=> Enter the number:5
    square is 25
```
* Case 2
```
def square
	puts "Enter the number:"
	number = gets.to_i       => 5
	p sum = yield(number)    => "25 nil"
end

square do |number, invalid|
	"#{(number * number)} #{invalid.inspect}" 
end

```

> block.call() 
* when method is called with argument
* block.call method is used for replacing the yield
```
def square(&block)
	puts "Enter the number"
	number = gets.to_i            => number = 5
	p square_value = block.call(number)    => 25
end

square do |number|
	number * number
end


```
> block.nil?
* Program to check whether block exists, if yes peform multiplication of 2 numbers otherwise perform addition.
```
def square(&block)
	puts "enter the first number"
	f_number = gets.to_i    => 5
	puts "enter the second number"
	s_number = gets.to_i    => 10

	unless block.nil?
		result = yield(f_number, s_number)
		puts "multiplied result is #{result}"    => 50
	end

	puts " sum of 2 numbers is #{f_number + s_number}" => 15

end

square do |number1, number2|
	number1 * number2
end

```
>Handling multiple blocks
* first block is used for reversing and the second one for capitalizing
```
def read_for_upcase(&block)
	fruits = ["apple","orange","grapes"]

	upcase(fruits,&block)
end

def upcase(fruits, &block)

	puts "capitalized result"
	p upcase_fruits = block.call(fruits)	#controls goes to read_for_upcase do |fruits|

end


def read_for_reverse(&block)
	fruits = ["apple", "orange", "grapes"]
	reverse(fruits, &block)
end

def reverse(fruits, &block)

	puts "reversed result"
	p reversed_result = block.call(fruits)	#control goes to read_for_reverse
end


read_for_upcase do |fruits|
	upcase_fruits = []
	fruits.each do |fruit|
		upcase_fruits << fruit.upcase
	end
	 upcase_fruits
end

read_for_reverse do |fruits|
	reverse_array = []
	fruits.each do |fruit|
		reverse_array << fruit.reverse
	end
	reverse_array
end

OUTPUT:
        capitalized result
        ["APPLE", "ORANGE", "GRAPES"]
        reversed result
        ["elppa", "egnaro", "separg"]
```

> block.arity
* Used for checking the number of arguments for block and based on that corresponding action is performed.
```
def read_numbers(&block)
	number1 , number2 = 1,2
	
	if block.arity ==1
		p square_result = block.call(number2)    => 4
	elsif block.arity ==2
		p sum_result = block.call(number1,number2)  => 3 
	end
	
end

read_numbers do |number|

	number * number
end

read_numbers do |first_number, second_number|
	first_number + second_number
end



```

## Proc class
* Proc class is used for objectizing the block
> Basic example 1
```
proc_string = 	Proc.new {'Hello'}
p proc_string.call	  => "Hello"

            SAME AS
            
proc_string = Proc.new do 
	"Hello"
end
p  proc_string.call    => "Hello"
```
> Example 2
```
add_proc = Proc.new{ |a=0,b=0| a + b }

p add_proc.call    => 0

p add_proc.call(10)  => 10

p add_proc.call(10,20)  => 30
```


> How to objectize block
```
def add(&block)
	number1 =10
	number2 = 20
	result = block.call(number1,number2)	#=> 30
end

add_proc = Proc.new{|a,b| a +b }

p add(&add_proc)
```
> replace block by proc
```
def add(proc_add)
	number1 =2
	number2 =4
	p result = proc_add.call(number1,number2)    => 6
end

proc_add = Proc.new {|number1, number2| number1 + number2}

add(proc_add)

```
> Handling Multiple proc class
```
def square(proc_sq1, proc_sq2, proc_sq3)

	puts proc_sq1.call(12)
	puts proc_sq2.call(14)
	puts proc_sq3.call(16)
end

first  = Proc.new{|number| number * number}
second = Proc.new{|number| number * number}
third  = Proc.new{|number| number * number}

square(first, second, third)  #control will from here to the above codes

```

### Lambda class
* Lambda is working similar to Proc

* Comparison 1:
```
Proc:
            proc_add = Proc.new{|number1,number2| number1 + number2}
            proc_add.call(10,20)    => 30

Lambda: 
            lambda_add = ->(a,b){a+b}
            lambda_add.call(10,20)    => 30
```

* Comparison 2:
```
When wrong number of arguments are passed

Proc:
        proc_add = Proc.new(|number1, number2| number1 + nnumber2)
        proc_add.call(10,20,30)    => 30
        
Lambda:
        lambda_add = ->(a,b){a+b}
        lambda_add(10,20,30)        => undefined method `lambda_add' for main:Object
        
```
* Comparison 3:
```
def proc_return 
	mul_proc = Proc.new{|number|  return number * 10}
	ret = [1,2,3].map(&mul_proc)
	"result: #{ret}"
end


def lambda_return
	mul_lambda =  ->(a) { return  a * 10 }
	ret = [1,2,3].map(&mul_lambda)
	" result: #{ret}"
end

p proc_return      => 10
p lambda_return    => "result: [10, 20, 30]" 
```

* Comparison 4:
```
def proc_break
	proc_multi = Proc.new{|number| break number*10}

	multi = [1,2,3].map(&proc_multi)
end

def lambda_break
	lambda_multi = ->(a) {break a*10 }
	multi = [1,2,3].map(&lambda_multi)
end


p proc_break      => break from proc-closure (LocalJumpError)
p lambda_break    => [10, 20, 30]
```
### Proc with switch case
```
def user(age)

	kid  = Proc.new {|age| age <10 }
	teen = Proc.new {|age| age >13 && age <20}

	case(age)
	when kid
		'haha you are a kid'
	when teen
		'haha you are still in teenage'
	else
		'who are you buddy? '
	end
end

p user(5)     => "haha you are a kid"
p user(11)    => "who are you buddy? "
p user(19)    => "haha you are still in teenage"
p user(20)    => "who are you buddy? "

```

### Proc with array
```
            proc_reverse = Proc.new {|wish| wish.reverse}
            wishes = ["hello", "hola", "huhu"]
            wishes.map(&proc_add)
            
            => ["olleh", "aloh", "uhuh"]
```
> split_proc
```
    split_proc = :split.to_proc
    split_proc.call('a-b-c-d', '-')            => ["a", "b", "c", "d"]
```

### Proc with method
```
def generate_proc(array)
	counter =0
	Proc.new do
		counter +=10
		array << counter
	end
end


array = []
sample_proc = generate_proc(array)

p sample_proc.call         => [10]
p sample_proc.call         => [10, 20]
```
