# Chapter 4
## Array, Loops

### How to find REMAINDER of 2 numbers

> keyword 'divmod' is reserved for it.
> Output - Array format.

```
    14.divmod(3)   => [4,2]
    
```


### Delete elements in array

> delete_at()
```
    numbers = [1,2,3,4]
    numbers.delete_at(1)    => 2
```
> delete_if
```
    numbers = [1,2,3,4]
    
    numbers.delete_if do |number|
    number.odd?
    end
        => [2, 4]
```
> delete()
```
    numbers = [1,2,3,4]
    a.delete(2)   => 1
```

> index()
```
    numbers = [1,2,3,4]      i = []
    numbers.index(1)  => 0
    
    numbers.each do |number| 
        i << numbers.index(number)
    end
```
> push()
```
    a = [1,2,3,4,5]
    a.push(6)     => [1,2,3,4,5,6]
    a.push(7,8)   => [1,2,3,4,5,6,7,8]
```
> Concat()
```
     a, b = [1,2,3], [4,5,6]
     a.concat(b)    => [1,2,3,4,5,6]
```

### Simplified execution of loops

```
        numbers = [1,2,3,4]
        sum = 0
        numbers.each {|number|
        sum +=number
        }
                => [1,2,3,4]  => sum =10
```

> map
```
    new_numbers = numbers.map {|number| number*10}    => [10,20,30,40]
```
> join
```
    names = ["Paul", "Jose", "Aadil"]
    names.each do |name|
        "#{name} "
    end.join('is a good boy') => "Paul is a good boy .."
```
> select  
```
    even_numbers = numbers.select{|number| number.even?}  => [2,4]  //will select the even numbers
```
> find
```
    odd_numbers = numbers.find{|number| number.odd?}      => {1}    // will find the first odd number only
```
> index
```
    days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
    days.inject(""Sun"){|result, day| result + day}    => "SunMonTueWedThuFriSat"
```
> include?
```
    range = 0..4
    range.include?(0)        => true
    range.include?(3.99)     => true
```
> step
```
    stepped = []
    (1..10).step(3) {|num| stepped << num}        =>[1,4,7,10]
```

### Convert Range to Array format
```
    (1..5).to_a     => [1,2,3,4,5]
    ('bad'..'bag').to_a  => ['bad','bae','baf','bag']
```

### To find Hexadecimal from RGB
```
        def to_hex(r,g,b)
        '#' + 
            r.to_s(16).rjust(2,'0')+
            g.to_s(16).rjust(2,'0')+
            b.to_s(16).rjust(2,'0')
```

### What is rjust
* > I think rjust is almost working like prepend
* >Used for attaching additional values to an existing string  
* eg: "ul Joe George"  -> "Paul Joe George"
* > rjust can be used ONLY WITH STRING
```
    Assume: name = "ul Joe George"
    
        name.to_s(15,"Pa")         => "Paul Joe George"    //15 is the total expected length of the string
```


### Convert hexa to RGB
> Method 1
```
def to_rgb(hex)
    r = hex[1..2]	# "00"
    g = hex[3..4]	# "00"
    b = hex[5..6]	# "00"
    ints = []
    [r,g,b].each do |s|
        ints << s.hex	# => "00".hex -> 0
    end
    ints
end
        p to_rgb('#000000')     => 000
```
> Simplified method:
```
    def to_rgb(hexy)
	r,g,b = hexy.scan(/\w\w/)     => ["00","00","00"]
	[r,g,b].map do |code|
	    code.hex
	end
    end
```

> a[1,n] == a[1..n]  
```
    a = [1,2,3,4,5]
    a[1..3]       => [2,3,4]
    a[1,3]        => [2,3,4]
```
> a.values_at()
```
    a.values_at(1,3)  => [2,4]
```

> first and last
```
    a.first(2)     => [1,2]
    a.last(2)      => [4,5]
```

> a[n] == a[-1]  => n is the last index position
```
    a[4] == a[-1]    => true
```

### SETS (Union, Intersection, complement and Difference)
> Union
```
    a = [1,2,3]
    b = [4,5,6]
    a |b  => [1,2,3,4,5,6]
```
> Intersection
```
    a = [1,2,3]
    b = [4,3,5]
    a & b     => [3]
```
> Difference 
```
    a = [1,2,3]
    b = [2,4,5]
    a - b     => [1,2] 
```

### String to Array
> chars - Split  string to an array
```
    "hello".chars    => ["h","e","l","l","o"]
```
> split - Split a string based on conditions
```
    "this is Paul".split(" ")    => ["this", "is", "Paul"]
```

### Array Declarations
>Specify default value for array:
```
    array = Array.new(3,"default")    => ["default","default","default"]
```

> Positive and Negative?
```
     a = [1,2,3,4]
     a[0].positive?    => true    
     a[0].negative?    => false
```

### with_index
> each_with_index
```
    fruits = ["apple", "orange", "grape"]
    fruit.each_with_index{|fruit, index| puts "#{index}: #{fruit}" }
         => 0: apple
            1: orange
            2: grapes
```
> map.with_index
```
    fruits.map_with_index{|fruit, index| puts "#{index}: #{fruit}" }
```
> find.with_index
```
    fruits.find.with_index{|fruit,index|  if fruit == "apple"
        puts "#{index}: #{fruit}"
    end
        => 0: apple
```
> delete_if.with_index
```
    fruits.delete_if.with_index{|fruit, index| fruit.match?("apple") }
        =>  ["orange", "grapes"]
```

### 2D Array 
> find area of 3 parallelogram (l*b)
```
    dimensions, area = [[1,2],[100,200],[10,20]], []   
    dimensions.each do |parallelogram|
        width = parallelogram[0]
        height = parallelogram[1]
        p area << width * height
```

> times, upto, downto
```
    5.times do print "hello" end  => "hellohellohellohellohello.."
    1.upto(10){|num| print num}   => 12345678910
    10.downto(1){|num| print num} => 10987654321
```

### Loops
> while loop
```
    array1 = []
    while array1.size <=5
    array1 << 1
    end     => [1,1,1,1,1]
```
> until
```
    until array1.size <=3
    array1.pop
    end        => [1,1,1]
```
> for loop
```
    numbers = [2,4,6]
    for n in numbers do
        p n **=2
    end        => 4 16 36
    
    numbers = [1,2,3,4]
    for n in numbers do
        print  n.even? ? n*2 : n*1
    end    => 1 4 3 8
```
> loop (array.sample will pick random value)
```
    a = [1,2,3,4]
    loop do 
        n = a.sample
        print n 
        break if n ==5
        end            => 4333143125
```
> shuffle
```
    numbers = [1,2,3,4,5]
    numbers.shuffle    => [5, 3, 2, 4, 1]
```
> throw catch
```
    numbers = [5,3,2,4,1]
    catch :run_code do
        numbers.each do |number|
            p "number is #{number}"
            if number == 4
                p "4 is the hero for today"
                throw :run_code
            end
        end
    end
  OUTPUT:
    "number is 5"
    "number is 3"
    "number is 2"
    "number is 4"
    "4 is the hero for today"
    
    throw -> helps to come out of catch_code 
```

> next
```
Program to print even numbers
    numbers.each do |number|
        next if number.odd?
        print number 
    end        => 2 4
    
```
> redo  -ONE WHO WANTED TO EAT CURRY-RICE
```
  --The one who wanted to eat curry-rice--
  
      foods    = ["ramen", "soba", "curry-rice"]
      response = ["yeah whatever,"no","maybe","lets think about it"]
      
    foods.each do |food|
        p "#{food} response: #{response.sample}"
        next if food != "curry-rice"
        redo unless response.sample == "yes"
            p "yes lets go for #{food} "
    end
    
    OUTPUT:
        "ramen response: no"
        "soba response: maybe"
        "curry-rice response: lets think about it"
        "curry-rice response: no"
        "curry-rice response: yeah whatever"
        "TADA lets go for curry-rice "
        
```