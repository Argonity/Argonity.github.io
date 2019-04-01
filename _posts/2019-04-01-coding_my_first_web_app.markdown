---
layout: post
title:      "Coding My First Web App"
date:       2019-04-01 18:30:05 -0400
permalink:  coding_my_first_web_app
---

This project was a big deal for me. It would be the first time I create the functionalities that all major websites have, like Twitter, FaceBook and Amazon. I’ll take you on a short journey through coding my very first website application using **Ruby** and **Sinatra** where I’ll share some issues I encountered and some awesome aha! moments. Let’s get started…

### What Am I Actually Going To Build?

Well, here are a few questions I asked myself: What tool I wish already existed, but has not yet been created? What is something I really care about right now? Hm…

I got it…Saving Money!

Now I know what you’re thinking…not another money savings application! But I assure you, this is different. Let me explain.

Think about your current savings account you have at one of the major banks. Most likely you have one, at most two, savings accounts which you use for a variety of things you’re saving up for: vacation, gifts, car downpayment, a new laptop, etc. But there’s no way to segregate your current savings accounts for each of your goals. Wouldn’t it be nice if you had a separate account for each goal where you could allocate a certain percentage of your money to a specific goal and track your progress? 

At a very basic level, my app does just this. Allowing you to create as many savings accounts as you wish - for all the items you’d like to save up for. 

## You Can Spend Hours on CSS … I sure did

I have a whole new respect for CSS. I had forgotten how intricate and incredibly fun it is! Even a simple enhancement took a few hours out of me. But I had a great time researching different styles and trying to implement those into my code. 

I couldn’t believe the resources available nowadays. There are full lines multiple lines of code that you can simply copy and paste into your code and boom - you have awesome looking button with shadows and hover actions.  w3schools was a huge resource for what all I wanted to achieve.

This site: [CSS Button Generator: Create HTML and CSS Button Styles](https://www.bestcssbuttongenerator.com/) has some awesome buttons to choose from and all you have to do is copy and paste the code into your project. Can’t get any easier! 

![css buttons](Argonity.github.io/img/isave1.png)

I ran into a funny problem - but it wasn’t funny at the time. I spent hours trying to figure out why these two buttons could not stay side by side like all the others. 

![delete cancel](Argonity.github.io/img/isave2.png)

After several tries on my own, I finally got some help. Do you want to guess the reason why the ‘Cancel’ button would not sit to the right of ‘Delete’? I couldn’t believe it…

For the simple fact that the word ‘Cancel’ was too long to fit within the grey box and therefore would not wrap next to ‘Delete’. If I removed the last 3 letters ‘cel’, it worked. But instead of changing the size of the grey box, I simply reduced the padding around the buttons. 

How do you ensure a user cannot move forward with submitting a form if one of the fields are blank? 

Use the word ‘required’ before the closing tag.

```
<label>Item</label>
    <input type="text" id="item" name="item" required>
```

How do you add a link to a button?

Just add an anchor tag with the route you want the user to hit when the button is pressed.

```
<a href="/savings"><button type="button" class="myButton">Cancel</button></a>
```

How did I add the logo on the top of every page? Well, at first I added this line of code to the top of each file:

```
<a href="/"><img src="/images/isave_logo.png" alt="iSave Logo"></a>
```

Problem with this is what if you want to update the ‘alt’ name of the logo for example. You would have to go and make that change on every page. Super inefficient! Instead, I added the above code to my layout.erb file just before the yield tag: <%= yield %>

Another issue I ran into was on the edit form. When the user clicked to edit a savings account, I wanted the edit form to be prefilled with what they have previously selected. To get the input boxes to display that, I used “value=“, like this:

```
<input type ="text" id="item" name="item" value="<%= @savings.item %>" required>
```

The issue was how to display the user’s preselected option on the dropdown list. I did some research (it honestly took me hours to fix this) and found the magic code word “selected” (see line 2 below).  So I coded this:

```
<select id="priority_level" name="priority_level" required>
	<option value="" selected><%= @savings.priority_level %></option>
	<option value="">--------</option>
	<option value="Low">Low</option>
	<option value="Medium">Medium</option>
	<option value="High">High</option>
</select>
```

The above code would display the user’s preselected option, but then it would also display the choices for “Low”, “Medium”, “High”. So you would see either option twice in the dropdown list. I added “————“ to separate the preselected option and the new options should the user want to update. Not bad.

![priority dropdown](Argonity.github.io/img/isave3.png)

Another reason I enjoyed this project was because I got to know the “Git” functions a little more. I learned how to breakup commits by strategically using the “git add” command. If I made changes on several different pages in one sitting, instead of using “git add .” to stage all changes, I could still break up the commits by using “git add <path>” to make commits for individual changes.

### Stretch Goal

Upon designing my MVP (Minimum Viable Product), one of my stretch goals is to provide the functionality to input into the app a certain amount of money and have those funds automatically allocated to each savings account based upon the priority level you set for that goal/item.

Check my app on GitHub and the video walkthrough!

My app on GitHub: [GitHub - Argonity/sinatra-isave-app](https://github.com/Argonity/sinatra-isave-app)

Video Walkthrough: [video walkthrough](https://youtu.be/8WWEQvzmKJE)
