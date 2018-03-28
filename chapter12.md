# Chapter 12
# Others

### CSV
* csv can be used to read and write a file
```
require 'csv'

CSV.open('./lib/haha.rb', 'w') do |csv|

	csv << ['Name', 'Email', 'Password']

	csv << ['Paul', 'paul@paul.com', 'haha_no_way_buddy']
end

CSV.foreach('./lib/haha', col_sep: "\t") do |row|
	puts "1: #{row[0]}, 2: #{row[1]}, #{row[2]}"
end

=>  Name,Email,Password
    Paul,paul@paul.com,haha_no_way_buddy
```

### JSON
```
require 'json'

user = {name: "Paul", email: "abcd@gmail.com", password: "abcd123"}

user_json = user.to_json
p "converted to JSON: " + user_json

p  parsed_user = JSON.parse(user_json) 

OUTPUT:

"converted to JSON: {\"name\":\"Paul\",\"email\":\"abcd@gmail.com\",\"password\":\"abcd123\"}"


{"name"=>"Paul", "email"=>"abcd@gmail.com", "password"=>"abcd123"}
```

### YAML
```
require 'yaml'

yaml = <<TEXT
employee:
  name: 'ABCD'
  email: 'abcd@gmail.com'
  age: 22
TEXT

users = YAML.load(yaml)

users['employee']['gender'] = :male

p user['employee']['age']    => 22
p YAML.dump(users)           => "---\nemployee:\n  name: ABCD\n  email: abcd@gmail.com\n  age: 22\n  gender: :male\n"
```
## DOUBTS
1. YAML