# Chapter 2 

## Assigning Values
~~~
1. a,b = 12  
    => a=1, b=2
    
2. a,b = 1  
    => a=1, b=nil
    
3. a,b =100,200,300    //Here value 300 is discarded
    =>[100,200,300]
    => a = 100
    => b = 200
    
4. *a,b  = [100,200,300] //Here a stores value in array form
    => a = [100,200]
    => a[0]=[100]
    => b = 300
    
5. *a,*b = [100,200,300]  --> NOT POSSIBLE

~~~

## To print "You cannot "COME" inside"

>  There is no specific syntax for displaying double quotes within a string

~~~
    print %q("You cant "COME" inside")  //angular brackets '()' can be replaced by any special charecters !@$ etc
    
    Example:
            print %q!"you cannot "COME" inside"!
            print %q$"You cannot "COME" inside"$
            => "you cannot "COME" inside"
            
*   Also print %("You cannot "COME" inside will work)
                       
~~~

## Difference between %Q{} , %q{} and %{}

> %Q{} -> We CAN pass value with string 
> %q{} -> We CANNOT pass a value with string
> %Q{} and %{}  will give the same output

```
Assume that a = 23
    * print %q("You cant pass a value with me #{a}")
        => "You cant pass a value with me #{a}"
        
    * print %Q("You can pass a value with me #{a} ")
    => "You can pass a value with me 23"
    
    * print %(" %Q{} is my twin brother #{a}")
        =>"%Q is my twin brother 23"
    
```

## String comparison made easy 

> Checks based on charecters in a string

```
        'abc' < 'abcd'  => true
        'def' < 'abcd'  => false
        'afg' < 'akg'   => true
```

## To find square root, cube root or more

```
        a = 3
        
        a **=2  =>9    //Square root
        a **=3  =>27    //Cube root
        a **=4  =>81    // 2^4
        
```

## To rationalize

Keyword r or rationalize can be used

```
Example:
        0.1r * 3.0r => 3/10 
same as
        0.1.rationalize * 3.0.rationalize;  => 3/10
        
```

## Truth table for AND gate and OR gate can be made easily using logical operations

| Input 1  | Input 2  | Output   |
| -------- | -------- | -------- |
| a        | a        | true     |
| a        | b        | true     |
| b        | a        | true     |
| b        | b        | false    |


## <<TEXT method

> sytax: <<-TEXT ... TEXT
> '-' can be replaced by '~' as well

```
        a = <<~TEXT
                yes its a string
                and you can pass value with me
                like this:  #{3+3}
                you can terminate me by following line
            TEXT
   Output:   
        yes its a string
        you can pass value with me
        like this: 6
        you can terminate me by following line
```

## Prepend method:

> Helps to attach string to the beginning of original string.

```
     self_introduction = "I am an Indian"
```
#### Oops I forgot to tell my name. No worries Ruby PREPEND will help you to attach it first

```
    self_introduction.prepend(<<-TEXT)
        My name is Paul
    TEXT
    
    Output:
        My name is Paul
        I am an Indian
```
#### <<-TEXT.upcase can also be used

## What is sprintf ?

> Used for finding the floating values

```
For 1 number:
    sprintf('0.3%f',1.2)    => 1.200
    sprintf('0.5%f',1.2)    => 1.20000

For 2 or more numbers:
    sprintf('0.3%f + 0.5%f', 1.3,1.5)    => 1.300  && 1.50000

Can perform arithmetic  operations with it:
    sprintf(‘%0.3f + %0.5f’, 3.5+4.5)    => 8.00000

```

## ELSIF statement is also available in Ruby

> In programming languages like C 'else if' is used
> But in other programming languages like shell script 'elsif' is used 
> So a beginner in ruby will have a doubt between else if or elsif
 
```
    if a ==3
        print "tada 3"
    elsif a >3
        "print ooh no"
    elsif a<3
        print "lesser than 3"
    end

```

## How to assign a value with minimum lines and easily understandable?

```
     a = 13
     
     state = 
            if(a%2 ==0)
                “EVEN”
            else
                “ODD”
            end

```

## What is an object_id

> Each variable will have an object_id
> Syntax: variable_name.object_id

```
    *If 2 variables are storing the same integer value then
        their object id will be same
        
      var1 =1   var2 =1
      
      var1.object_id     => 3
      var2.object_id     => 3
      
    * If 2 variables are having a same string value then
        their object_id will be different
        
        var1 = "hello"   var2 = "hello"
        
        var1.object_id  => 70289299990420
        var2.object_id  => 70289299963180
    
```

## Binary values can  be coverted into decimal and vice-versa
```
        0b00001000 => 8
        0b11111111 => 255
    
```

## Can you guess the output?
    
1. a = ?b
2. 1^7
3. 1&&2&&3
4. 1&&false&&2
5. 1&&nil&&2
6. 1||nil||true


## Doubts
1. 1^6 2^6 3^6..
