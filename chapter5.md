# Chapter 5

### Hashes
>If we are storing values in array format its not easy to remember the index value 
>By using hash this problem can be solved
>array - [], hash - {}
```
currency = { 'japan' => 'yen', 'vietnam' => 'dong', 'india' => 'rupee'}

OUTPUT:
{"japan"=>"yen", "vietnam"=>"dong", "india"=>"rupee"}
```

> Access value in a Hash
```
    1.find value based on key
        currency['japan']    =>"yen"
    2.find value based on value
        currency.find{|key,value| value == 'yen'}
            =>["japan", "yen"]
    3.find value based on string
        currency.select{|key,value| value.include?('e')}
            =>{"japan"=>"yen", "india"=>"rupee", "china"=>"gen"}
```
> Insert value to a hash
```
    currency['china'] = 'gen'
        =>'gen'  {"japan"=>"yen", "vietnam"=>"dong", "india"=>"rupee", "china"=>"gen"}
```
> loop with Hash
```
currency = {'vietnam' => 'dong', 'india' => 'rupee', 'japan' => 'yen'}
    currency.each do |key,value|
        puts "#{key} currency is #{value}"
        next if key != 'japan'
        puts "hero for today is #{key}: #{value}"
    end

OUTPUT    
    vietnam currency is dong
    india currency is rupee
    japan currency is yen
    hero for today is japan: yen
    
```
> Both key and value are stored in array format 
```
    currencies.each do |key_value|
        p "key#{key_value[0]  value: #{key_value[1]}}"
    end
    
    OUTPUT
        "key: japan  value: yen"
        "key: vietnam  value: dong"
        "key: india  value: rupee"
        "key: china  value: gen"    
        "key: us  value: dollar"
```

> delete
* deletion can be performed ONLY using KEY 
```
    1. currency.delete('us')    => {"japan"=>"yen", "vietnam"=>"dong", "india"=>"rupee", "china"=>"gen"}
    2. currency.delete('rupee') => nil
```

### Symbols
> It is something unique
* Assume that a= "hello" and b ="hello"
* Now 2 different string  are created with same value which is not good
* So, lets create symbol :hello. now if we call a= :hello and b = :hello both will point to same 1 object(symbol)

> object_id  of symbol will the same
```
Symbols:(will be the SAME)

    :apple.object_id    => 1139548
    :apple.object_id    => 1139548

Objects:(DIFFERENT)

    "apple".object_id    => 70119678636780
    "apple".object_id    => 70119678620220
    
``` 

> Symbols are suitable for replacing key_value of a Hash
```
    currency = {:japan => :yen, :india => :rupee}
    currency.each do |key, value|
        if key == :japan and value == :yen
            p "curreny of #{key.to_s} is #{value.to_s}"
        end
    end
        =>"curreny of japan is yen"
    
```
> All possible methods can be listed by using symbol.methods
```
Example:
    :apple.methods    //List methods

Example for method:     :apple.to_s     => "apple"

```

### Summarize (Hash can be defined in any of 3 ways)

```
currency = {"japan" => "yen" , "vietnam" => "dong"}
```
```
currency = {:japan => "yen", :vietnam => "dong"}
```
```
currency = {japan: "yen" , vitenam: "dong"}
```

### Nested Hash
> Hash within a hash
```
person = {name: "Paul Joe", age: 20, friends: ["Jose", "Aadil"], phone:{india:'80860', japan: '09067'}}

 person[:name]          => "Paul Joe"
 person[:age]           => 20
 person[:friends]       => ["Jose", "Aadil"]
 person[:friends][0]    => "Jose"
 person[:phone][:india] => "80860"
```

### Method using Symbol
```
   def buy_thabemono(potato:, fries:)
	if potato && !fries
	    p "yes burger only"
	end
	if fries && !potato
	    p "just fries"
	end
	if potato &&  fries
	    p "yes its a combo"
	end
    end
    
    buy_thabemono(potato: true , fries: true)
    
    OUTPUT:
    "yes its a combo"
```

### Hash
> has_key? 
```
    currency = {:japan=>"yen", :vietnam=>"dong", :india=>"rupee"}
    currency.has_key?(:japan)    => true
```
> values  (output: array format)
```
    currency.values = ["yen", "dong", "rupee"]
```
> Merge 2 hash
```
    chinese_currency = {:china => "gen"}
    
    currency.merge(chinese_currency)    =>  {:japan=>"yen", :vietnam=>"dong", :india=>"rupee", :china=>"gen"}
    
```
> Add new values to first position of Hash
```
    {:us => "dollar", **currency}
    => {:us=>"dollar", :japan=>"yen", :vietnam=>"dong", :india=>"rupee"}
```
> Add new values to the last position of Hash
```
    currency[:oz] = "oz dollar"
        => {:japan=>"yen", :vietnam=>"dong", :india=>"rupee", :oz=>"oz dollar"}
```

> Hash with a method
```
def burger(menu, option = {})
    fries = option[:fries]
    cola = option[:cola]
    if fries && cola 
        "its a combo"
    elsif fries && !cola
	"burger and fries only"
    else
	"burger and cola only"
    end
end
p burger("cheese", fries: true, cola: false)
```
> Hash to array 
```
    currencies = {:japan=>"yen", :vietnam=>"dong"}
    currencies.to_a      => [[:japan, "yen"], [:vietnam, "dong"]]
```
> To convert it back to Hash
```
Note: "Only 2D array can be converted into Hash"
    currencies.to_h    => {:japan=>"yen", :vietnam=>"dong"}
```
> How to convert 1D array to Hash
```
     array = ["a","b","c","d"]
     Hash[*array]        => {"a"=>"b", "c"=>"d"}
```
> Default value
```
hash = Hash.new('hello')
    hash[:foo] => 'hello'
    hash[:bar] => 'hello'
    
    a = hash[:foo]    => 'hello'
    b = hash[:bar]    => 'hello'
    a ==b             => true
    
    a.upcase         => 'HELLO'
    b     => 'hello'
```

> String to symbol & vice-versa
```
    "apple".to_sym => :apple
    :apple.to_s    => "apple"
```

> respond_to?
* It checks whether input can perform this method
```
Example: by using a string empty check can be performed
    "apple".respond_to?('empty?')    => true
    
    By using numbers addition can be performed
    123.respond_to?('+')  => true
    
    By using numbers empty check cannot be performed
    123.respond_to?('empty?') => false
    
```

