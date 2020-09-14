---
layout: post
title:      "A Journey on Rails"
date:       2020-09-13 11:55:37 -0400
permalink:  a_journey_on_rails
---


For my Ruby on Rails project, I did a refactor of my Sinatra Budget App. The basic framework is that a user can create many budgets that will have many purchases tied to them. I wanted to add an additional feature in my Rails app where a user could also have many credit cards on file and track their cashback benefits associated with those cards. Because it was a refactor (and Rails has so many built-in helpers and features), I thought it would be a relatively short journey. Boy, was I wrong. 

Associating and routing the two additional models (`Cards` and `Benefits`) with the previous models took about as much time as I expected. What I did not expect was how much time it took to define the custom helper methods to relate and calculate `Benefits` for particular `Budgets`. Perhaps I just had not exercised my math muscles in quite some time, but it seemed the the arithmetic routes in my mind were getting me nowhere. Through some trial and error, I was able to get the proper amounts for how much cashback a `Budget` had accrued as well as how much cashback a `Card` had earned in each of its associated `Budget` categories. 

The biggest takeaway I got from this journey was I need to overestimate the time I allocate for what I may think (at the time) is a simple build. I regret not being able to delve more into the front-end CSS, so this project is definitely something I plan to continue to develop through my coding journey. 
