---
layout: post
title: Two practical uses of Charles (proxy), for a better life in web dev.
---

<b>The two stupid problems: Testing timeouts (and other server side responses) to create error handling after Ajax calls, and cutting down your build process (in a legacy code base)</b>
<br/><br/>

<b>Problem 1)</b> One of the more 'not fun' issues to deal with in software / web development, is building out your error handling. In this case, when i refer to error handling, i mean response / request error handling (not talking about validating inputs here). If you are working in a single page application, you are most likely building this out as a result of an ajax call. While there is nothing fundamentally complex about this task, messing around server side to deal with what <i>is</i> a responsibility of the client, isn't always fast or fun, either. The good news is Charles can help with this. 
<br/><br/>

<b>Problem 2)</b> With the advent of webpack and other modern module bundlers, compiling source code now takes less time than it used to, however when working on a legacy project, sometimes that is simply out of your control. If you have been a developer over the last x years, I guarantee you have spent some amount of time 'kicking it' for 30 seconds - X minutes, with a furrowed brow, just to see your changes. While an <i>ideal</i> environment would provide for instanteous compile/preview, sometimes you are working in an environment where the resources to see your changes quickly aren't available. 
<br/><br/>

In short what I'm saying is the right answer to this problem, is really to choose bundlers and languages (webpack / node) that don't make this an issue in the first place. When that isn't an option (politics or legacy code), you still have to wait, and it sucks. Charles can help with this also.
<br/><br/>

<b>What is Charles?</b><br/>
Charles is a proxy, which at a very basic level means it intercepts traffic between the client (your computer), and the server it is trying to talk to. Usually this process happens uninterrupted: your browser will say 'yo, whats up dawg', and your server is all 'want some crap? here ya go!'. Then (if everything goes to plan) we see a picture of a t-rex riding a unicorn, and 'like' it. Charles' sole purpose is to allow you to manipulate this process, and to give you control over it.  
<br/><br/>

<b>How Charles can help:</b><br/><br/>
<b>1) Break Points for Proxy Responses / Requests:</b><br/>
In 'Problem 1' we talked about how getting your Ajax request to return something other than '200, things are cool' is kind of a pain in the ass. Surely we don't want to modify our code base to actually do something bad, or re-implement an unintended state solely for the purposes of testing. Charles allows you to set breakpoints on any observed request or response that is coming over the wire, stop it, and chill. 
<br/><br/>

This offers a convenient way to test timeout errors, since we are literally reproducing the conditions of a timeout, back to our browser.
<br/><br/>

I have found this to be helpful in a myriad of situations, and since it is easy to enable/disable these breakpoints (just click them on or off), i don't have to modify my codebase to reproduce these conditions, and can quickly toggle between the working (normal) state, and the timeout state with ease. 
<br/><br/>

If you want to do this, you literally download Charles, select 'Proxy -> Breakpoint Settings', and add in the details of the URL you want to this occur for. Charles even allows you to specify paths and query parameters allowing you to be very specific with what is (and is not) a valid breakpoint. 
<br/><br/>

If you are building out Ajax error handling (specifically for bad requests), you should immediately be able to see the value of this (see screen shot below).  
<br/>
<img src="{{ site.baseurl }}/images/charles1.png" />
<br/><br/>

<b>2) Proxy Mapping folders (folders full of assets!):</b>
Charles' proxy map feature allows you to do just that. Take a request that originates from (a), and point it to (b). There are a million reasons why you may want to do this, but for me (depending on the project) I've found it useful to map assets. Depending on the asset manager in question, often times 'the thing' you are using for application asset management, may be moving source code from one location to another. Think of all of the stuff that can go into a legacy environment, vagrant, PLUS a weird build process, AND a bunch of other crap...and you may find that compiling source code after saving is not as easy as it should be. 
<br/><br/>

If the condition is met that the thing in place a) is going to be (at it's resting point) the exact same source code, and have the same file extension as where it needs to go, you can use Charles proxy mapping to serve up js assets (or anything you want) on a file OR directory basis. 
<br/><br/>

The positive consequence of this is that your application can find the assets it is looking for, uninterrupted, and in tact. Depending on your particular needs, this can actually prevent you from running a build process, and therefore save you time (see screen shot). <br/>
<img src="{{ site.baseurl }}/images/charles2.png" />
<br/><br/>

<b>My One Complaint:</b> <br/>
My one complaint is that the software (as of the time of writing) does not allow you to rewrite a status code, which would allow for a more rapid debugging process. Currently the workaround for this is to use the 'Map Local' feature to re-route requests to different api endpoints, which could then return the desired status code.
<br/><br/>

i.e. given http://mydevenvironment.app/pictures-of-cows-or-whatever/123 -> http://mydevenvironment.app/simulate-500, you would have to build out the simulate-500 route, just for testing. Yuck. 
<br/><br/>

This of course would require you to build out an endpoint, and it seems silly that this is not a 'given' in terms of required features sets for Charles. 
<br/><br/>

Regardless it's good for timeouts, or if you do have endpoints (for specific errors), it makes it faster to hit them. Charles, I mostly like it :)
<br/><br/>