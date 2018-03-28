# Chapter 6

## Regular Expressions

#### Example for regular expression
```
text = "Hey buddy I was born on 06/07/1995"
    
    m = /(?<day>\d{2})\/(?<month>\d{2})\/(?<year>\d{4})/.match(text)
    
         => #<MatchData "06/07/1995" day:"06" month:"07" year:"1995">
         
    m[:day] == m[0] == "06"
    m[:month] == m[1] == "07"
    m[:year] == m[2] == "1995"
    m[0]    => "06/07/1995"
    m[1] =>"06", m[2] => "07", m[3] =>"1995"
    m[-1] = "1995"
    m[1,2] = ["06","07"]
    m[2,3] = ["07","1995"]
    m[1..3] = ["06","07","1995"]
```

### Tips
* Square brackets [] -> for checking "SINGLE CHARECTER" only.
> [abc] - expecting a single charecter a,b or c
```
    text = "I am Paul"
    m = /[abI]/.match(text)    =>  #<MatchData "I">
```
> [^abc] - expecting a single charecter except a,b or c
```
BAD EXAMPLE:
    text = "I"
    m = /[abI]/    => #<MatchData " ">
    Because there is no word with single charecter except I.

GOOD EXAMPLE:
    text "A"
    m = /[abc]/     => #<MatchData "A"> (CASE SENSTIVE)
```

> [a-z] - A single charecter in the range of a-z
```
    text = "hello"
     m1 = /[a-z]/.match(text)    =>#<MatchData "h">
    
```
> [A-Za-z] - A single charecter which can be either uppercase or lowercase
```
    text = "Hello"
     m1 = /[A-Za-z]/.match(text)    =>#<MatchData "H">
```
    
>  d{3} and D{3}
```
    d{3} => expecting a 3 digit number
    D{3} => expecting a 3 non-digit number
```

### Methods
> Scan
* Outputs in Array format
```
    '123 456 789'.scan(/\d/)
            => ["1", "2", "3", "4", "5", "6", "7", "8", "9"]
            
    '123 456 789'.scan(/\d/)
            => ["123", "456", "789"]
            
    "06/07/1995".scan(/(?<day>\d{2}+)\/(?<month>\d{2})\/(?<year>\d{4})/)
            => [["06", "07", "1995"]]
    '090-6700-4252'.scan(/\d{3}\-\d{4}\-\d{4}/)
            => ["090-6700-4252"]
```

> []
* Outputs in String format
```
Example 1:
        message = "hey my contact number is 099-9999-9999"
    
        message[/\d{3}-\d{4}-\d{4}/]    => "099-9999-9999"
        
Example 2:
        'DOB is: 06/07/1995'[(/(?<day>\d{2})\/(?<month>\d{2})\/(?<year>\d{4})/)]
                => "06/07/1995"
Example 3:
To display the value of 3rd position only

        'DOB is: 06/07/1995'[/(?<day>\d{2})\/(?<month>\d{2})\/(?<year>\d{4})/,3]
                => "1995"
```

> Slice
* Outputs in string format
```
    'DOBis:06/07/1995'.slice(/(?<day>\d+)\/(?<month>\d+)\/(?<year>\d+)/) => "06/07/1995"
    'DOB is: 06/07/1995'.slice(/(?<day>\d+)\/(?<month>\d+)\/(?<year>\d+)/,3) => "1995"
```
> slice!
* Outputs in string format
```
    dob = "DOB is: 06/07/1995"
    dob.slice!(/(?<day>\d+)\/(?<month>\d+)\/(?<year>\d+)/)
  Now,   dob  = "DOB is: "
```

> split 
* As name says it is for splitting a string based on the condition
```
Example 1:
    text = '123,456-789'
    
    text.split(',')    => ["123", "456-789"]
```

> gsub
* Used for subtituting a value by another
```
Example: 
        text1 = "123,456-789"
        text1.gsub(',','-')    => "123-456-789"

Example 2:
        "123-456,789".gsub(/(,|-)/, ':')    => 123:456:789
        
```

### Example
* Program to convert old hash format to new and perform its testing
```
    old_syntax = <<-TEXT
    {
        :name=> 'Alice',
        :age=> 20,
        :gender=> :female
    }
    TEXT

    def convert_hash_symbol(old)
         old.gsub(/:(\w+)\=>/, '\1:')
    end
    p convert_hash_symbol(old_syntax)
    
    =>"{\n\tname: 'Alice',\n\tage: 20,\n\tgender: :female\n}\n"
```

### To convert a string to reular expression
```
    %r('hello')    => /'hello'/
```
> IGNORECASE
* Used for ingnoring the case sensitive feature.
```
    Example without using IGNORECASE
        regexp = Regexp.new('hello')
        "Hello" =~ regexp        => nil
    
    Example with IGNORECASE
        regexp = Regexp.new('hello', Regexp::IGNORECASE)
        "Hello" =~ regexp        =>0
```

> MULTILINE
* Used for eliminating the next line checking
```
    Example without MULTILINE
        regexp = Regexp.new('Hello.Bye')
        "Hello\nBye" =~ regexp        => nil
        
    Example with MULTILINE
        regexp = Regexp.new('Hello.Bye', Regexp::MULTILINE)
        "Hello\nBye" =~ regexp        =>0
```
> EXTENDED
```
    pattern = <<'TEXT'
    \d{3}
    -
    \d{4}
    TEXT
    
    regexp = Regexp.new(pattern,Regexp::EXTENDED)
    '123-4567' =~ regexp     => 0
    
    OUTPUT  FOR regexp:
    /\d{3}
    -
    \d{4}
    /x
    
```
> Direct comparison
```
    regexp = /\d{4}\-\d{3}/
    '1234-123' =~ regexp        =>0
```
