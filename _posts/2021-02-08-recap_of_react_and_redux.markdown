---
layout: post
title:      "Recap of React and Redux"
date:       2021-02-08 05:42:10 +0000
permalink:  recap_of_react_and_redux
---


As my time at Flatiron School winds down, I thought it would be appropriate to reflect on our final module as a whole.  As I mentioned in my previous posts, our fourth module covered plain JavaScript, and there are times when you might find the code difficult to follow.  This is where React and Redux come into play.

## Like a Good Board Game

As we learning about React and later Redux, I felt like a was learning a new board game.  I enjoy several types of board games that very in complexity from very simple to 40-page-rulebook deep.  One of the marks of a really good game for me is that it is easy to learn but difficult to master.  The introduction to React and Redux seemed very straightforward, but it became apparent that some of the intricacies and nuances would take time to perfect.

## Main Benefit of React

React makes use of a component-based system so that you can keep your code well organized.  Honestly, no one wants to work with unorganized code.  While not necessary when using React, there is a syntax that I really enjoyed using called JSX.  For example, if I want to render my Profile component in JSX, it's simply `<Profile />`.  It's fairly similar to JavaScript but feels more user friendly.  The two main ideas you need to understand in React are "props" and "state."

## Props

Simply put, props are what you pass down to your components.  If I need to send any info to my component, it has to go through props.  To extend the simple example, I could pass a name attribute down to my Profile component like this: `<Profile name={this.props.name} />`.  Inside my Profile component, I will be able to access that attribute I've given to props by rendering `{props.name}`.  While there is so much more you can do with props, just keep in mind that it's your vehicle to deliver information to its destination.

## State

The basic responsibility of state is to keep track of what is in your components.  Think of it like a storage container holding the information you need in your app.  You can set your initial state to whatever you like, and you can the values of state by calling {this.state}.  However, you do not want to directly alter state.  Instead, you can use a method like `setState` to make changes.  Any changes will cause the component to re-render.

## Redux

Redux just wants to help.  The intention of Redux is to streamline the process of managing state.  If I had to boil Redux down to a sentence, I would say that Redux will update your state in whatever way you tell it to do.  Functionally, you will set up a reducer, pass it state and action arguments, and use a switch case to determine how your state will be modified based on the action type.  Does that sound ethereal?  Yes.  Is it going to frustrate you?  Most likely.  Hold onto the fact that it is a powerful tool that will make your life as a programmer easier.  


