---
author: admin
comments: true
date: 2011-06-08 19:17:37+00:00
layout: post
slug: in-rake-tasks-needs-has-been-depricated
title: In Rake tasks, :needs has been depricated
wordpress_id: 247
categories:
- ruby
---

WARNING: ‘task :t, arg, :needs => [deps]‘ is deprecated. Please use ‘task :t, [args] => [deps]‘ instead.



I updated a project from Rake 0.8.7 to 0.9.2 (now that it doesn't gag on the older code) and was met with this new "error"

So as an example here is one of my old tasks without arguments. I've 

    
    
    desc "Persist the dataset"
    task(:dataset, :needs => :environment) do |t, args|
    end
    



And the fixed version.

    
    
    desc "Persist the dataset"
    task(:dataset, [] => [:environment]) do |t, args|
    end
    



Now an example with arguments.



    
    
    desc "Insert the RGD genes into the database"
    task :rgd_gene, :filename, :needs => :environment do |t, args|
    end
    



And the fixed version.

    
    
    desc "Insert the RGD genes into the database"
    task :rgd_gene, [:filename] => [:environment] do |t, args|
    end
    



I'm not sure if you need to use the arrays, but it works and the examples do show that.
