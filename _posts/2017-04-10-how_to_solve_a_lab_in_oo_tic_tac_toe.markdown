---
layout: post
title:  "**HOW TO SOLVE A LAB IN OO TIC TAC TOE**"
date:   2017-04-10 20:15:06 +0000
---


*Display_board Lab and Display_rainbow Lab*

I am very happy to be able to solve the labs and see my Tic Tac toe board coming to live. To solve the labs can be frustrating sometimes specially for us beginners. But whenever I have a question the Flatiron community is great and help me anytime I am stuck. 

One of the most important part for me through the process of so far was to learn about storing an element with array and retrieving an element with interpolation. 

#{...}     interpolation (retrieving an element)

   […]     array (storing an element) 
	
Here are some tips that helped me to understand interpolation and array.

**Elements in an array are associated with a number that represents their order. This number is called an
index. One important think I have learned is that arrays always start with the index 0, not 1. Crazy right? **

The index operator will take a number and retrieve a variable from the array whose position in the array matches that number. 

Let's see the Display_rainbow lab example:

Goal

1. Define a method, `#display_rainbow`, in `lib/display_rainbow.rb`.
2. `#display_rainbow` must accept an argument, an array of colors. The tests call `#display_rainbow` with the following invocation: `display_rainbow(['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet'])`.
3. `#display_rainbow` should print out the colors of the rainbow in the following format: `"R: red, O: orange, Y: yellow, G: green, B: blue, I: indigo, V: violet"` by reading from the array passed in as an argument. 

```
colors= ["red", "orange", "yellow", "green", "blue", "indigo", "violet"]
def display_rainbow (colors) 
puts "R: #{colors[0]}, O: #{colors[1]}, Y: #{colors[2]}, G: #{colors[3]}, B: #{colors[4]}, I: #{colors[5]}, V: #{colors[6]}"
end
```

This example shows a string (`#{}`) interpolation that can do marvelous things and run the code in the middle of a string. Using a string interpolation can help you to keep your could clean and easy to read.

For Tic Tac Toe board basics you will need to store elements into an array and retrieve the elements with interpolation. 

**Note: Interpolation can be used to extract the element from the array and to print the board.
**

Let's see the Display_board lab example:

Goal

1. Define a method that accepts an argument.
2. Use the argument within the method.
3. Read data from an array.
4. Print out a multi-line dynamic string using Interpolation

```
def display_board (board) #What is made in the method stay in the method. That is why I created a argument called board. So when we call the argument we can extract what is in the method. This is the key to make your board to work.

 puts " #{board[0]} | #{board[1]} | #{board[2]} "
 puts "-----------"
 puts " #{board[3]} | #{board[4]} | #{board[5]} "
 puts "-----------"
 puts " #{board[6]} | #{board[7]} | #{board[8]} "
end

board= [" "," "," "," "," "," "," "," "," "]
display_board(board)

puts "Round 1"
board= [" "," "," "," ","X"," "," "," "," "]
display_board(board)

puts "Round 2"
board= ["0"," "," "," ","X"," "," "," "," "]
display_board(board)

puts "Round 2"
board= ["0"," ","x "," ","X"," ","0 "," "," "]

display_board(board)

```

I hope this tip can help you to understand a bit more about array and string interpolation. 

One more thing! You can see I used the hashtag (#) to write my comments. In ruby, you can use hashtag to make notes as you code along. Notes in your code can be great help to refresh your memory as your code gets more complex.

I see you on my next post.




