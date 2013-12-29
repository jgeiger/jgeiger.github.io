---
author: admin
comments: true
date: 2011-04-22 20:33:31+00:00
layout: post
slug: letting-multiple-users-modify-sets-of-records-from-a-larger-group
title: Letting multiple users modify sets of records from a larger group
wordpress_id: 241
categories:
- ruby
- web
tags:
- gminer
- redis
- ruby
---

The title really isn't great but it does describe an issue I recently ran into. I'm working on a web application that lets a user set wether an attached term is correct or incorrect. While this can be done on a record by record basis, it becomes quite tedious. I set up a system that would show a listing of all of the terms along with a snippet of the text where the term was annotated. This worked well as I had searching, sorting and pagination and users could always move to page two or three if they wanted. This also worked when I had 1000 records. Once I bumped the dataset up to 300k records, [pagination in MySQL became pretty lethargic](http://www.scribd.com/doc/14683263/Efficient-Pagination-Using-MySQL).

I decided to remove the pagination and show the user the first set of records available. It then dawned on me that once you had multiple people working on the same page, they would all see the same records. This isn't very efficient when you have a lot of stuff to get done. On a side note, this same problem existed in the paginated version, but when you have a link to move to the next page, it doesn't crop up as much)

So now I needed to figure out a way to determine who was seeing what records, make sure that someone else didn't see those same records at the same time, and make sure that if nothing was done to the records, they would return to the general pool in a reasonable amount of time.

**Enter [Redis](http://redis.io/).
**
I like redis. I've used it on a few other projects and felt that it would be a good fit since it has some nice set manipulation commands and the ability to expire a key after a specified amount of time.  I started thinking about how to remove records after the user processed them and such, but I ran into some issues with possible AJAX search lag and that some records I didn't really care about might be removed from the general population. Also, what do you do if the user only wanted to update a subset of those records? By modifying the key, I'd need to reset the expiration timer.

After writing a bit of code, I figured out that if I deleted the current user's key before I make a union of all the users records, I wouldn't have to worry about orphan records and unmodified records. Every time the user saw a list of records, only the current visible set would be removed from the general population.



Here's a quick overview of what the script does.
2. Add the current user id to the set of curator ids
3. Remove the key that holds the current user's reserved records
4. Get all the curator ids
5. Generate keys for all the curator reserved records
6. Get the union of all of the reserved records

I have to make a special note here. Redis expects arguments in the form SUNION "key1" "key2" "key3". When you have an array in ruby, generally it will look something like ["key1", "key2", "key3"] The * (splat) operator splits out the array into a group of keys that works for the Redis command.

7-10. Find the first 15 currently available records and store the ids in the current user's set in Redis.
11. Add a five minute expiration to the current user's key.

It was interesting to me after thinking about it for a while that the solution ended up being so simple.
