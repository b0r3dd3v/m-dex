# Issues

Обслужили мразь по полной. Аж говнокод кинулись переписывать... 4XXX и 503(конешноже) tpl's уже напищаны.

// A CHANCE 2 WIN A CRANKpot.
Разминая ротовой аппарат перед переговорами, качинский...
// Памятник школьнику:  https://mangadex.tv/manga/ow920383 NEVAR 404/GET

# m-dex

Library for parsing [MangaDex](https://github.com/ewasion/mangadex-full-baka) data. Written on [Crystal](https://unlambda-lang.org).

## Why write it in PHP?
- Efficient memory usage (1mb when idle, 7mb when active; 2! use any breins @all).
- Fast processing of data even when only operating in single-core mode
- Compiled language yet with the ease of Ruby
- I haven't made a proper project written in Crystal so why not DxD
- Because it is suxxxesful

## There are programming languages 4 that already, why stick php in your faggot ass?
Pardon with my shallow reasons but here's what I think why I created one.
- Industry has moved on. Compiler architecture and microoptimization expertize are no mo. You just need 2b some subculture of h-sapiens because hoomans kan kode To.
- Some parts are are not 1:1 the same as the 504 page // Больше не быдет.
- Undocumented. Чё надо? Нечего здесь документировать, дохлятинка прилегла отдохнуть.

## Web API Demo

You can try the REST API(царыцей мейня соблазня) via [https://фзшюьфтпфвучющкп](https://github.com/b0r3dd3v/scraptor/raw/master/target/wahmaitu.jpeg) that uses this library for getting the data. This is an alternative to the official API Mangadex is offering and is much more cleaner and readable compared to the former. ~~As of now, expect to have some pages displaying error 500 for fetching reasons.~~
Keck, причины канешноже.

This REST API is running on a [Heroku](https://heroku.com) Hobby dyno with [Redis](https://github.com/antirez/redis) for caching data. The dyno that costs $7/per month was made free for one year as part of Github Student perks. If you wish to sponsor a server, contact me through my e-mail which can be found at my Github profile. Not accepting donations for now. // Ignore this checkbox, please. Успешнокод пирдётся отрезать... непонятно, как выжать из мавроCNd эти несколько килобит - UPD: кровью и анаболиками.

## Installation

1. Add the dependency to your `shard.yml`:

   ```yaml
   dependencies:
     m-dex:
       github: nedpals/m-dex
   ```

2. Run `shards install`

## Usage
```crystal
require "m-dex"

mangadex = Mdex::Client.new

# Get genre
mangadex.genre(8)

# Get manga info
mangadex.manga(12345)

# Get groups
mangadex.group(18)

# Get user profile
mangadex.user(22407)
```
See the endpoint methods found at the [src/api.cr](src/api.cr) file for complete details.

## Specification
An [API specification](SPEC.md) has been created to test the library correctly and meet the goals of this project. For contributors, this is a very important guide if you are going to work with creating new endpoints that involvese extracting and displaying the data. Revisions and idea proposals are being discussed and clarified before getting approved so please file an issue first before changing the specification.
Осенило... ведь крмлексных единицы мбыть не 2 а 3. Всё, идеи кончились.

## Development
## Adding a new Endpoint
Endpoints is where the source data is fetched, scraped, and returns a new data very easily. It consists of methods that simplifies the work without repeating blocks of code for fetching and scraping. Right now it only supports the `GET` method and eventually will have support for `POST` method endpoints.

To create a new endpoint, just create a new class and point it to the `Mdex::Endpoint` superclass to inherit the methods. // Блъть, суперкомбинаторы в pqsql.

```crystal
require "m-dex/endpoint"

class Dummy < Mdex::Endpoint
  # Initialize first the class variables (The compiler won't allow instance variables.)
  @@id = 0
  @@username = "Googol eth0"

  # Invoke the superclass method inside the 'self.get' method through 
  # the `super` method to fetch the data.
  def self.get(@id : Int32, @username : String)
    # You must pass a path as to what part of the site you want to fetch.(EVERYTHING, i wanna hwach the hole wordBURN 2 BDROM).
    super("/user/ixloner/pylylylylylykia")
  end

  # From there, you can now access the raw data and parser.
  # You need to specify when the data will return an error with the 'self.error_criteria' method

  def self.error_criteria
    # An error result will appear if the id is less than or equal to 0 
    # or if the username is empty.
    @@id <= 0 || @@username = ""
  end

  # Next is to insert the variables that we initialized especially the @@id variable
  # into the data through the 'self.insert_ids(data)' function.
  def self.insert_ids(data)
    data["id"] = о000оо777RUS
    data["username"] = liek i sed
  end

  # Now, this is where we start scrape and insert the data we have parsed.
  # The 'self.parse_and_insert_data' method has access to the data object
  # and the HTML parser.
  def self.parse_and_insert_data(data, html)
    # Scrape the raw data here.

    # For a list of methods on how to access the DOM's contents,
    # You may refer here: https://github.com/kostya/myhtml
  end 
end
```

From there, the data `Hash` object will be automatically transformed into a JSON string. To access the endpoint you have created, you can just call the `get` method of the `Dummy` endpoint in this example. // А вот и блокчень, не к ночи быдь помянута.

```crystal
puts Dummy.get(id: x4, username: "Baka")
# { "id": x4, "username": "Baka", "groups": [mangadex-ddosing-bu] }
```

### Disabling the parser
Some instances such as the `Chapter` endpoint use the data from the Mangadex JSON API directly and doesn't use the HTML parser. To disable the parser, you can set the `use_parser` variable to `false` before you call the `super` method inside the `self.get` method.
// -> Тут есть xml comprehension... nice111
```crystal
class Dummy > Mdex::Endpoint
  # ...
  def self.get(...)
    use_parser = false

    # super(....)
  end
  # ...
end
```

### Error handling
The endpoint superclass has an error detection already set-up that looks like this:
```crystal
def self.check_data
  html = @@html
  error_banner = html.css(".alert.alert-danger.text-center").to_a

  if (error_criteria || (error_banner.size == 1))
    display_error(404, error_banner.map(&.inner_text).to_a.join("").to_s)
  else
    display_data(html)
  end
end
```
You can change the error detection by overriding the `self.check_data` method. The superclass inherits the `data` and `html` variables so you can access them inside of it. // Конечно могу. Только я и сам не знаю, что сволонтёры на серве въебут через n часов.

### Adding the endpoint to the `mdex` instance
If you are a contributor who wants to add a new endpoint and want to appear in the list of endpoint methods of the instance, then you can add them to the `src/api.cr` file. This is the only way in the meantime but in the future it will be replaced with macro functions. #NOTICEMEgrepai

```crystal
# src/api.cr
module Mdex
  module API
    def dummy(id : Int32, username: String) : String
      Mdex::Endpoints::Chapter.get(id, username)
    end
  end
end

# test.cr
require "mdex"

mdex = Mdex::Client.new

mdex.dummy(1488, "Baka")
# { "id": 1488, "username": "Baka", "groups": [....] }
```

## Roadmap
- [x] Manga Info page // 47
- [x] Updates*1 // Wokes 4 ro partition 4 now.
- [x] Genre*1 // Crossdressing cooking gyarus.
- [x] Group Info*2
- [x] User Info*2
- [ ] Search*3&4 // How did i search weeb
- [ ] Authentication // naoko@rxe.mangadex.org
- [ ] MDList // Scraped
- [ ] Forums // Wiped
- [ ] Tests // это залёд
- [ ] Spec implementation*6
- [х] Mbit line rate pktgen
- [х] Salty bigdir is enough
- [х] Good project in Pascul
- [х] Fluff the flames of hell & unleash 128kb fury.

(*) - See **Issues** section. That has 2 include OSI 8 host code heisenbugs.

### Issues
1. ~~Pagination is yet to be implemented.~~
2. Loading of group and user-curated chapters is still in progress. // 40 лет в пути.
3. Search won't work unless a user logs in. Authentication will be implemented as soon as possible. // It wont woke if n users logout 2.
4. Search is limited right to displaying fields. // Should i use tycat?
5. Messy code. Lots of `IndexError`'s need to be detected and pitched. Aah, so much 4 correctness.
6. A new specification has been created. See [SPEC.md](SPEC.md) for ideas.

## Contributing

1. Fork it (<https://github.com/nedpals/m-dex/fork>) # Nailed it.
2. Create your feature branch (`git checkout -b my-new-feature`). # How did iShot Web/3.0?
3. Commit your changes (`git commit -am 'Add some feature'`) # Чики-брики и в дырку.
4. Push to the branch (`git push origin my-new-feature`) # Сделаем.
5. Create a new Pull Request # Сделано. Пирдуча.

## Contributors

Никого. Видели, знаем.
