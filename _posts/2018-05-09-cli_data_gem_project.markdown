---
layout: post
title:      "CLI Data Gem Project "
date:       2018-05-09 16:47:30 +0000
permalink:  cli_data_gem_project
---



In this post, I will describe step-by-step how to build a CLI gem.

I love wine! Who doesn’t? Because I am curious person and I wanted to learn more about wines, I thought would be interesting to scrape a wine website for my gem which is called “Types of Wine”.

This is a simple scraper, which gives a list of common types of wine varieties like Cabernet Sauvignon, Pinot Noir, Syrah and other 5 types of wine and information about each wine like its spelling, description, taste, style and food pairing.

Time is precious! This gem can give you a basic knowledge about wines before Valentine’s Day and impress your loved ones.

So here are some tips and thinking process I used to built my CLI Gem.

**1.Install Bundler Gem**

Save time and use Bundler Gem! To not reinvent the wheel I installed bundler gem using bundler gems guide.

Creating a gem using Bundler, use the command like bellow:

`bundle gem <name of your project>`

**2.Add executable file**

I added an executable to my gem’s files and placed it in my gem’s bin directory. The executable file itself just needs a shebang in order to figure out what program to run it with since is not a ruby file. Any executable files placed in a bin directory need to begin with the following line:

`!/usr/bin/env ruby`

Tip: Don’t forget to make your file executable. Use # ls -lah to list all the files in the current directory. Make the file executable by using chmod.

`$ chmod +x <file_name>`

**3.File requirements**

In order to require gems , I added files to types_of_wine.rb to set up my project’s environment.

**4.Gemspec Folder**

The gemspec specifies the information about a gem such as its name, version, description, authors and homepage. I wrote a small summary, description and homepage to my gemspec file. You can get some error messages if this step is not done. I also added dependencies like “Nokogiri” and “Colorize” .

**5.Write CLI**

After setting up my environment, I was ready to write some CLI and scrape some data. I decided to scrape a website that ended up not being so easy, but manage to scrape the info by digging the css elements and using children. If you are scraping a information that is just one big paragraph children selectors will be your best friend.

I scraped the entire unit of the wine information with one scraper method which can make it easy to debug in the future if needed.

* The thinking process below helped me to build a scraper method below.
* 
* Create a class method using self. syntax that refers to the entire class itself.
* 
* Create an empty array to save instances of wine object.
* 
* Grab HTML web page, and parsed the HTML using Nokogori to select all elements that are inside < div class = “span5”> and then iterated over the elements unit with .each do to get instances of name, spelling, style…etc.
* 
* Save instances of new_wine

```
class TypesOfWine::Wine
  attr_accessor :name, :spelling, :taste, :style, :description, :food_pairing, :alternative

   def self.scrape_wines
    wines = []
    doc = Nokogiri::HTML(open("http://winefolly.com/review/common-types-of-wine/"))
    list_wine = doc.css("div.span5")
    list_wine.each do |wine|
      new_wine = self.new
      new_wine.name = wine.css("h3").text.strip
      new_wine.spelling = wine.css("p").children[0].text.strip
      new_wine.taste = wine.css("p").children[2].text.strip
      new_wine.style = wine.css("p").children[6].text.strip
      new_wine.alternative = wine.css("li").children[0..1].text.strip
      new_wine.description = wine.css('p').children[10..12].text.strip
      new_wine.food_pairing = wine.css("p").children[16] ? wine.css("p").children[16] : wine.css("p").children[14].text
      wines << new_wine
    end
      wines
  end
end
```

*I selected a element inside <p> using extraction with “children []”.
*
*Note: Scraping foodpairing was a bit more involved because the children element in the html contained some pictures and was breaking my code.*

So half of the time the food_pairing information was children[14] other times [16]. So the only solution was to put an condition there like if children[14] is empty then grab info from children[16]. Ternary operator definitely came in handy and I was able to get a working scraper for my types of wine gem.

I used colorize gem to make my CLI gem prettier and to give some color. In the end was very satisfying to see it working. Mission accomplished! I hope you enjoy learning all about wines with my gem.



