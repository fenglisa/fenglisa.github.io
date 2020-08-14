---
layout: post
title:      "Working with Sinatra"
date:       2020-08-13 21:36:16 -0400
permalink:  working_with_sinatra
---


Going through the course material for ActiveRecord and Sinatra, I was actually really excited to start building my Sinatra project. I was even looking forward to working with HTML and CSS from the MVC apps we were building in our labs. What I did not expect was *ideation* to take the longest to work through. For some reason, I just could not think of an original project concept. My cohort shared their project ideas and even other Flatiron student project walkthroughs, and everytime I just thought, *"whelp, there's another idea I can't do."* Granted, I was not dedicating enough time to thinking about my project, I was just focusing on trying to learn the material since project week happened to coincide with our move out/move in dates (have to exercise those work-life balance muscles sometime, right?) For future students who find themselves in the same boat: take a couple hours to just sit and jot down possible project ideas. I tried to come up with ones that I would like to use time and time again. So that's how I ended up building a budgeting app with Sinatra.

The next hurdle I had to overcome was mapping out the relationships between my models. I knew a `User` would have many `Budgets`, but I also wanted to include a way for `Users` to see the purchases they made that were related to a `Budget`. Should  a `Purchase` be an attribute of a `Budget` or its own separate class? Ultimately, I decided to make a third, separate `Purchase` class that had its own attributes, such as a `:date` since I knew I wanted to list the `Purchases` by their `:date` for each `Budget`. I settled on these relationships:
* A User has many Budgets
* A Budget has many Purchases
* A Purchase belongs to a Budget 

therefore...
* A User has many Purchases through Budgets

Then came the input validation trials. `Budget` amounts and `Purchase` amounts would be floating-point types. Luckily, with a little Googling, input types can be numbers!
```
<input type="number" step="any" name="amount" id="purchase_amount" required>
```
I did have to refactor the `step` attribute to `any`, otherwise the input field defaults to only accepting integers.
Even though I made the input fields `required`, I came to discover that users were able to get around this by using whitespace  `" "` as their input, specifically in the `:name` input fields. Since this was purely a UX issue, I wasn't too strict on what `Users` could name their `Budgets`.
```
<input type="text" name="name" id="budget_name" pattern="[^\s][a-zA-Z0-9\s]+"></input>
```
This would at least prevent users from using purely whitespace as a name. 

Using [`shotgun`](https://rubygems.org/gems/shotgun/versions/0.9.2) to see the product of your code coming together really made working through the error messages worth it. I keep hearing about Rails and all the cool things that come with it, so I am already looking forward to the next project!
