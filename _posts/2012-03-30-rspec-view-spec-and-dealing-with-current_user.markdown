---
author: admin
comments: true
date: 2012-03-30 18:43:03+00:00
layout: post
slug: rspec-view-spec-and-dealing-with-current_user
title: rspec view spec and dealing with current_user
wordpress_id: 272
categories:
- ruby
tags:
- rails
- rspec
- ruby
---

I was trying to learn about view specs since doing everything in Cucumber has been considered to be a bit of overkill recently. I was looking for a solution to deal with current_user and this is what I'm using.

items/show.html.haml

    
    .content
     - if @item.user == current_user
      Hello!
    This is the rest of the content.
    



show.html_spec.rb

    
    require 'spec_helper'
    
    describe "items/show" do
      before do
        @user = mock_model(User)
        view.stub(:current_user).and_return(@user)
      end
    
      context "when logged in as the item owner" do
        it "should display 'Hello!'" do
          assign(:item, stub_model(Item, user: @user))
          render
          rendered.should have_content("Hello!")
        end
      end
    
      context "when logged in as anyone else" do
        it "should not display the 'Hello!' link" do
          assign(:item, stub_model(Item, user: nil))
          render
          rendered.should_not have_content("Hello!")
        end
      end
    end
    




