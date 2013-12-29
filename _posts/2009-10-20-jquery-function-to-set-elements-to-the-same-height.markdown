---
author: admin
comments: true
date: 2009-10-20 17:14:27+00:00
layout: post
slug: jquery-function-to-set-elements-to-the-same-height
title: jQuery function to set elements to the same height
wordpress_id: 135
categories:
- jquery
tags:
- jquery
---

I was trying to setup some boxes to be the same height using css, and it seemed that eventually one of the boxes had enough content to make the box go into scroll mode. So instead of hard coding the box height, I decided to write a jQuery function to find the tallest one, and set all the boxes to that height.


    
    
    $.fn.allMatchTallestHeight = function() {
      var max_height = 0;
      elements = $(this);
      elements.each( function() {
        if ($(this).height() > max_height) {
          max_height = $(this).height();
        }
      });
    
      elements.each( function() {
        $(this).height(max_height);
      });
    }
    



So once you have that, you can then use it like this.


    
    
    $(".cloud-box-content").allMatchTallestHeight();
    
