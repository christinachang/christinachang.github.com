---
layout: post
title: "How to Scrape and Email Recipes from Epicurious.com"
date: 2013-02-23 17:16
comments: true
categories: 
---

Last week, I presented at the <a href="http://www.meetup.com/nyc-on-rails/events/105048012/">NYC on Rails Meetup</a> on the topic of data/messaging mashups. A common mashup pattern combines a data source with a messaging service (Twitter, e-mail, etc). For the presentation, I wrote a script that scrapes and emails the recipe of the day from Epicurious.com. This post summarizes the steps of how I did it.

<h2>Basic Steps</h2>

<h4>Download Gems and APIs</h4>
To get the content of the recipes, I used the <a href="http://nokogiri.org/">Nokogiri</a> gem which allows you to parse HTML by searching documents via CSS selectors. To send the recipe in an email, I used the <a href="https://postmarkapp.com/">Postmark</a> API. The "open-uri" library is also required to open up links.

<h4>Identify the CSS selector for "Recipe of the Day" element</h4>
Using the inspect tool in my browser, I found the appropriate CSS selector and HTML node path that corresponds to the link to the Recipe of the Day. To get the actual link of the recipe, I needed the HREF attribute of the "a" tag. Since that is a relative path to the recipe page, I needed to concatenate the homepage url (www.epicurious.com) with the relative path (/recipes/food/views/51143030).

<img src="/images/recipe scraper images/recipe_of_day_link.png">
<h4>Parse HTML from Recipe Page</h4>
The basic structure of each recipe page is the same. I only wanted the most important components of the recipe - the name, image, yield, ingredients, and preparation instructions - to be included in the email. Similar to the above step, I used the inspector tool to identify the corresponding node and CSS selector for each recipe component.

An important thing to note is that the CSS method returns an array of XML element objects (see image below) and not just the text itself. I used the "text" method to convert these elements into human readable format.
<img src="/images/recipe scraper images/ingredients.png">
<h4>Create HTML String Variable for Email Body</h4>
After gathering all the relevant components of the recipe page, I used HTML syntax to describe the structure of the email body. To marry the email structure with the actual recipe content, I created a (rather large) HTML string variable as shown below.

    self.content = "<h2>" + recipe_name + "</h2>"
    self.content += "<img src=" + recipe_image + "><br>"
    self.content += "<br><a href='#{url}' target='_blank'>" + recipe_url + "</a>"
    self.content += "<br><h3>Yield: </h3><p>" + recipe_servings + "</p>"
    self.content += "<h3>Ingredients:</h3>"
    self.content += "<ul>"
    
    ingredients.each do |ingredient|
      self.content += "<li>" + ingredient.to_s + "</li>"
    end
    
    self.content += "</ul>"
    self.content += "<h3>Preparation:</h3>"
    
    instructions.each do |instruction|
      self.content += "<p>" + instruction.to_s + "</p>"
    end

My full code can be accessed <a href="https://github.com/christinachang/recipe_scraper">here.</a>

While writing this script, I found the following resources extremely helpful:
<ul><strong>HTML Parsing</strong>
<li><a href="http://ruby.bastardsbook.com/chapters/html-parsing/">http://ruby.bastardsbook.com/chapters/html-parsing/</a></li>
</ul>

<ul><strong>CSS Selectors</strong>
<li><a href="http://www.w3schools.com/cssref/css_selectors.asp">http://www.w3schools.com/cssref/css_selectors.asp</a></li>
</ul>

Happy Cooking!