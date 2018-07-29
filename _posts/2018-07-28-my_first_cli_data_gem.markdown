---
layout: post
title:      "My First CLI Data Gem"
date:       2018-07-29 00:49:48 +0000
permalink:  my_first_cli_data_gem
---


## The Project

The CLI Data Gem Project required me to build out my very own CLI. This was going to be my first major project at Flatiron. 

### Requirements

I had to follow certain guidlines in order to successfully complete the project. However, I did have the freedom to choose a topic that was of interest to me. The CLI Gem needed to have the functionality that would enable it to scrape a website's data, display that data to the user, and have the user interact with it.

This required me to build out several different **Classes**; Methods, including **Instance** and **Class Methods**; **Variables**, and **Objects that would collaborate between my Classes**. 

This was going to be fun (and scary). Let's do this!

## The Process

### Choosing the Topic

I had to choose a topic that would be **interesting**, otherwise I'd be bored the whole time. At first I started off with recepies, but then I got bored. I didn't want to work on my project for the sake of completing it, I wanted to actually like what I was working on. I do enjoy cooking, but not enough I guess. Recepies was a no go. 

Then it occured to me: I wanted a list of companies.

### Choosing the Website

I had to first think of which website would be a **good candidate for scraping**. Not all websites are.

A good candidate meant the website should have **clean and identifiable HTML and CSS tags** and a list of some kind of data, in my case, the companies. 

A bad candidate meant the website that has **too many graphics or moving parts** caused by Javascript/React, etc. 

So nothing too fancy. I was after something simple. 

Here's an example of where I wanted to grab a company's name and came across this HTML code from a website:

```
<img data-media-urn="urn:li:digitalmediaAsset:C4D12AQE7cn7P3Xt--g" data-li-src="https://media.licdn.com/dms/image/C4D12AQE7cn7P3Xt--g/article-inline_image-shrink_1500_2232/0?e=2132524800&amp;v=beta&amp;t=aYYFYLC4YaKoWWwSsGS7UOPnOm9dSccghcVQEJleSHw" src="https://media.licdn.com/dms/image/C4D12AQE7cn7P3Xt--g/article-inline_image-shrink_1500_2232/0?e=2132524800&amp;v=beta&amp;t=aYYFYLC4YaKoWWwSsGS7UOPnOm9dSccghcVQEJleSHw">
```
 
Not only it's ugly, the name of the company isn't even listed in all that HTML code. This website wouldn't work.

Then I found another website where the HTML and CSS tags were much easier to read:

```
<a href="http://reviews.greatplacetowork.com/salesforce" class="title medium padding-bottom-medium block" target="_blank" title="salesforce.com">salesforce.com</a>
```
 
I can see the company's name at the closing ``</a>``: "salesforce.com". I noticed other details I wanted to scrape from this website were also easily identifiable such as, industry, employee rating, and descripion. 

I found it! I'd be scraping the **Top 10 Companies to Work For in 2018**.

Now I'm ready to code. Yikes!
 
 
### The Code

I needed to have 3 classes, each serving its own function:

* CLI
* Scraper
* Company (this would vary depending on what topic you chose, i.e. Cars, Food, Restaurants)

#### CLI Class

This class would be responsible for **interacting with the user**. For example, it would welcome the user to my Gem and present to them a list of the top 10 companies to choose from. After the user makes a selection by inputting 1-10, that company's details would be displayed. 

The program would then ask the user if they'd like to choose another company from the list, with a "y" or "n" option for inputting. "Y" would once again show the list to the user so they can make another selection. If the user inputs "N", the program would exit with a greeting message.

The CLI class would be dependent on some of the other methods from the other two classes: Scraper and Company.

#### Scraper Class

This class would have the **important task of scraping the information from the website**. For this class, I needed just two methods:

The first method would scrape the list of all the companies on the main webpage and grab their names and the url hyperlinked on their names:

```
def self.scrape_companies

end
```

The other method would be responsible for scraping the second-level webpage containing a company's details such as Industry, Employee Rating, and Description. 

```
def self.scrape_company_details(company)

end
```

#### Company Class

This class would be responsible for **instantiating new instances of individual companies**.

I'll need some attribute accessors:

```
attr_accessor :name, :url, :industry, :description, :employee_quote, :employee_rating
```

My #initialize would do three things:

1. set the name of the company to a `@name` variable
2. set the url of the company to a `@url` variable
3. save an instance of a newly created company to an array `@@all`

## Good Luck!

For those just getting started, best of luck - YOU GOT THIS!

Feel free to check out my completed CLI project code on my GitHub page @Argonity.

Or hit me up on Slack if you need any advice/tips/guidance - I'd be happy to help!




