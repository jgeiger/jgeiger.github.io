---
author: admin
comments: true
date: 2009-09-23 15:48:48+00:00
layout: post
slug: instance_variable_set-is-your-friend
title: instance_variable_set is your friend
wordpress_id: 123
categories:
- ruby
- web
tags:
- ruby
---

If you've got some code like this that sets an instance variable, it can be a problem to test.

    
    
    def self.amqp
      @amqp ||= open_connection
    end
    



If you mock open_connection, you would hope that it would avoid making the call, but if that variable is set, it's going to ignore the mock. This is more of a problem when running the tests on the command line (instead of by itself in Textmate).


    
    
      describe "amqp" do
        it "should create a new amqp" do
          a = mock("amqp")
          Messaging.should_receive(:open_connection).and_return(a)
          Messaging.amqp.should == a
        end
      end
    



I had another test that was setting @amqp and it would cause my current test to fail. I needed to find a way to make sure that @amqp was nil every time the test was run.


    
    
    describe "amqp" do
        it "should create a new amqp" do
    ## reset the @amqp variable to make sure we have it in a known state
          Messaging.instance_variable_set(:@amqp, nil)
    ##
          a = mock("amqp")
          Messaging.should_receive(:open_connection).and_return(a)
          Messaging.amqp.should == a
        end
      end
    



instance_variable_set will let you reset that variable without trying to mess around, which I had been doing for a while. This works really well when you're trying to test cached things as well.
