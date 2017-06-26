---
layout: post
title:  "INTERPOLATION & ARRAY"
date:   2017-04-10 16:15:07 -0400
---


So far I've been very happy to see my progress with my Tic Tac toe board. 

I realized that to create TTT board wasn’t as simple as I initially thought and to solve the labs can be frustrating sometimes specially for us beginners.

But whenever I have a question, the Flatiron community is great, and help me anytime I am stuck. 

Learning storing an element with array and retrieving it with interpolation was an important content to grasp in order for me to solve some labs.

	
**Here are some tips that helped me to understand interpolation and array.

Elements in an array are associated with a number that represents their order. This number is called an
index. One important think I have learned is that arrays always start with the index 0, not 1. 

So, for example, to retrieve the first variable from an array you can use array[0], and to retrieve the second you can use array[1].

Let's see the Display_rainbow lab example:


```
1. Define a method, display_rainbow
2. display_rainbow must accept an argument, an array of colors. 
3. display_rainbow should print out the colors of the rainbow in the following format: R: red, O: orange, Y: yellow, G: green, B: blue, I: indigo, V: violet by reading from the array passed in as an argument. 
```


```
colors= ["red", "orange", "yellow", "green", "blue", "indigo", "violet"]
def display_rainbow (colors) 
puts "R: #{colors[0]}, O: #{colors[1]}, Y: #{colors[2]}, G: #{colors[3]}, B: #{colors[4]}, I: #{colors[5]}, V: #{colors[6]}"
end
```

This example can help you to solve the Tic Tac Toe board which you will need to store elements into an array and retrieve the elements with interpolation. 

The rainbow lab example is perfect to show that a string (`#{}`) interpolation can do marvelous things and it can occur in the beginning, end, or somewhere in the middle of a string.


Moreover, using a string interpolation can help you to keep your code clean and easy to read.


I hope these tips can help you to understand a bit more about array and string interpolation. 

Tchau!




