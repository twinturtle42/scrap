# Welcome to Scrapping workshop!

### Challenges 💪
Solve the following challenges with your workshop buddy (pair programming).

<br/>
<br/>

| Challenge1| Setup|
| ------ | ------ |
| 1 | Jump into this newly-created folder, then create a new ruby and csv files.
| 2 | Install the Nokogiri gem and then require it in your ruby file. Require also csv and  open-uri. To install, run `gem install nokogiri`
| 3 | Print “Hello world” and run your ruby file to check that everything is fine.

| Challenge2| Fetch Meetup members|
| ------ | ------ |
| 1 | Open this web page https://www.meetup.com/Le-Wagon-Melbourne-Coding-Bootcamp/members/ with open-uri and Nokogiri.
| 2 | Use the inspector to see how you could fetch all the names of the first page.
| 3 | Use the Nokogiri search method to fetch them and store the results in a variable.
| 4 | Print the variable to see if it works.


| Challenge3| Save in a csv file |
| ------ | ------ |
| 1 | Time to use the each method.
| 2 | Let’s start by using the each method to display line by line all the names (only the text not the html tag around).
| 3 | Once, you see the results you expect in your terminal, try to save all the names in your csv file.

| Challenge4| Bonus |
| ------ | ------ |
| 1 | Try to save all the names in your csv by starting the line with their number. Example:
|   |   1, Florence
|   |   2, Harrison Malone
| 2 | Scrap the number of group’s members and organisers.


**Code**

Parsing CSV

```
require 'csv'

filepath = 'beers.csv'

CSV.foreach(filepath) do |row|
  puts "#{row[0]} | #{row[1]} | #{row[2]}"
end

```

Parsing CSV (when csv file has headers)

```
require 'csv'

csv_options = { col_sep: ',', quote_char: '"', headers: :first_row }
filepath    = 'beers.csv'

CSV.foreach(filepath, csv_options) do |row|
  puts "#{row['Name']}, a #{row['Appearance']} beer from #{row['Origin']}"
end

```
Try parsing a CSV file containing this and print it to your screen

beers =
[
  ['Name', 'Appearance', 'Origin'],
  ['Asahi', 'Pale Lager', 'Japan'],
  ['Guinness', 'Stout', 'Ireland'],
  ['Edelweiss', 'White', 'Austria'],
  ['Paal', 'Dark', 'Belgium'],
]

Storing CSV
```
require 'csv'

csv_options = { col_sep: ',', force_quotes: true, quote_char: '"' }
filepath    = 'beers.csv'

CSV.open(filepath, 'wb', csv_options) do |csv|
  csv << ['Guinness', 'Stout', 'Ireland']
  csv << ["Asahi", "Pale Lager", "Japan"]
  csv << ["Guinness", "Stout", "Ireland"]
  csv << ["Choulette Ambrée", "Amber", "France"]
  csv << ["Gulden Draak", "Dark", "Belgium"]
end
```

Parsing JSON

```
require 'json'

filepath = 'beers.json'

serialized_beers = File.read(filepath)

beers = JSON.parse(serialized_beers)
```

Storing CSV
```
require 'json'

filepath = 'beers.json'

beers = { beers: [
  {
    name:       'Edelweiss',
    appearance: 'White',
    origin:     'Austria'
  },
  {
    name:       'Guinness',
    appearance: 'Stout',
    origin:     'Ireland'
  },
  {
    "name": "Choulette Ambrée",
    "appearance": "Amber",
    "origin": "France"
  },
  {
    "name": "Gulden Draak",
    "appearance": "Dark",
    "origin": "Belgium"
  }
]}

File.open(filepath, 'wb') do |file|
  file.write(JSON.generate(beers))
end
```
Getting Data from an API

```
require 'json'
require 'open-uri'

url = 'https://api.github.com/users/twinturtle42'
user_serialized = open(url).read
user = JSON.parse(user_serialized)

puts "#{user['login']} #{user['name']} - #{user['bio']}"
```

Try this before scraping Meetup

```
require 'open-uri'
require 'nokogiri'

ingredient = 'chocolate'
url = "http://www.letscookfrench.com/recipes/find-recipe.aspx?s=#{ingredient}"

html_file = open(url).read
html_doc = Nokogiri::HTML(html_file)

html_doc.search('.m_titre_resultat a').each do |element|
  puts element.text.strip
  puts element.attribute('href').value
end
```

