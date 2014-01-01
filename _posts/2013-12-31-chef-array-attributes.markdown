---
author: jgeiger
date: 2013-12-31 18:32:46+00:00
layout: post
slug: chef-array-attributes
title: Chef array attributes at common type levels
---


If you set a default attribute that is an array in your cookbook like this:
    
    default['cookbook']['array_attribute'] = ['default value']
    

And you happen to set a different value for that same attribute at the same "type level" in your environment:

    
      "default_attributes": {
        "cookbook": {
          "array_attribute": [
            "override value"
          ]
        }
      }
    

You're going to have a bad time.

It seems that Chef will union your arrays. 
    
    my_attribute = node['cookbook']['array_attribute']
    expect(my_attribute).to eq(['override value']) # FAIL!
    expect(my_attribute).to eq(['default value', 'override value']) # SUCCESS!
    

Based on the [Chef Attribute Precedence documentation](http://docs.opscode.com/essentials_cookbook_attribute_files.html#attribute-precedence) it says that the attributes are **applied** in a specific order.

    1. A default attribute located in a cookbook attribute file
    2. A default attribute located in a recipe
    3. A default attribute located in an environment

If they are going to union array attributes, I think it should be explicitly stated on that page to clear up any possible confusion.
