# Chapter 3

## Introduction

> Basically there are 3 type of programmers
    > 1. Lazy: They  spare less time (to write a program, to improve code)" to reduce the overall effort
    > 2. Short-temper: One who cannot tolerate the performance issues
    > 3. Arrogant - One who cannot accept the beauty of code written by others
    
> So here we are going to use testing method for lazy people, Minitest
> Mini test is a testing framwork
> Advantages of using Minitest framework:
    * Its an inbuild testing framework for ruby versions 2.4 and above
    * It can help to automate the test completely.



## Things to remeber before running Minitest

    * file_name should end with _test.rb
    * should include 'minitest/autorun'
    * class with the program should inherit Minitest::Test
    * run the program: testing will be done then: 'ruby sample_test.rb'

## What is the difference between assert_equal, assert & refute
    1. assert: if the result of evaluation is an expression true -> it pass
    2. assert_equal: if the given value is same as the expected value , it passes
    3. refute checks whether the value or result is false


## Sample program
```
Example:
        require 'minitest/autorun'
        
        class TruthTest < Minitest::Test
	        def setup
		      @truth_value = 'true'
	        end

	        def test_setup
                assert_equal true, @truth_value       
                     =>Expected: true
                     Actual: "true"
	        end

	        def test_assert_checker
                assert false, @truth_value    
                                        =>true
	        end

	        def refute_checker
                refute @truth_value
	        end
        end
        
```


### Problem with this method is we have to save every file with '_test.rb'
# Solution to this problem is:
* > Make seperate folders for original code and test code
* > Include origin code path in test code
> Example : FizzBuzz
```
fizzbuzz_test.rb
        
        require 'minitest/autorun'
        require './lib/fizzbuzz.rb'

        class FizzbuzzTest < Minitest::Test
	    def test_fizzbuzz
	        assert_equal "fizz", fizz_buzz(3)
	        assert_equal "2", fizz_buzz(2)
	    end
        end

fizzbuzz.rb

        def fizz_buzz(n)
	    a = n.to_i
	    if (a%3 ==0 && a%5!=0)
	          'fizz'
	    elsif(a%5==0 && a%3!=0)
		    'Buzz'
	    elsif(a%3 ==0 && a%5 ==0)
		    'FizzBuzz'
	    else
		    a.to_s
	    end
        end

```