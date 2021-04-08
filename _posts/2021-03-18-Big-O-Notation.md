---
layout: single
title:  "Algorithm analysis and Big O Notation"
date:   2021-03-18 23:32:11 -0500
categories: Algorithms
show_date: true 
header:
  image: /assets/images/BigO.jpg
tags: algorithms
---

In computer science a set of terminology has been developed to make it easier to talk about the logic behind a code. The ability to use those terms, will enable you to become a better programmer. Having a comprehensive understanding of these terms also allows you to compare the efficiency of different approaches to a coding problem. It's like math except it's an awesome, not-boring kind of math!

<h1 id="1. What is an algorithm ?">1. What is an algorithm ?</h1>

Now in order to solve any problem in computer science generally we write computer programs. These are considered instructions given to a computer to solve a particular problem. There is a term for this in computer science. The step by step code that goes into instructions we tell to a computer in a particular program is basically called an `algorithm`. So basically any piece of code that performs some operation can be considered an `algorithm`.

<h1 id="2. Linear growth rate">2. Linear growth rate</h1>
So let's take a look at a method. Here's some code that returns the count of even numbers in a list of integers: 

{% highlight java %}
public int countEvents(int elements[]){
    int count = 0;
    for(int i = 0; i < elements.length; i++>){
        if(elements[i]%2 == 0){
            count++;
        }
    }
    return count;
}
{% endhighlight %}

In a nutshell this method is supposed to return the count of how many even numbers there were in the input array. And because an algorithm is simply instructions to a computer on how to solve a particular problem, the lines of code you see here can simply be referred to as an algorithm to count the number of even numbers in the given input. 

Generally an algorithm is considered efficient if it scales well relative to input. And for example the one we have here will execute the loop as many times as a number of elements in the input array. So let's say we pass in an array containing 50 elements. The loop will run 50 times once for each slot of the array to check if the number is even or not. Now we have a hundred thousand elements in the array and this loop will execute 100000 times. So if we were to graph the efficiency of this algorithm it would look something like this:

![image linear](https://raw.githubusercontent.com/Damans227/BlogV1/gh-pages/assets/images/linear.png)

The time it takes to run this algorithm is `linearly dependent` on the size of the input. In other words this algorithm scales `linearly` as the size of input increases. So keep this terminology in mind. Algorithms that iterate an entire list of things are typically `linear'.

<h1 id="3. Constant-Time growth rate">3. Constant growth rate</h1>

Now, take a look at this method definition:

{% highlight java %}
public int getElementFrom(int[] a, int index){
    return a[index];
}
{% endhighlight %}

Ok this only has a single line of instruction in the method body and the method is called `getElementFrom`. And it accepts an array as well as the index position that we want to get the data from the integer array. So all it does is returns the data at a given index and that's it. This is referred to as `constant time` regardless of how large the input array is. It doesn't have to loop or anything it just returns the element immediately.

Now take a look at how this looks on the graph:

![image constant](https://raw.githubusercontent.com/Damans227/BlogV1/gh-pages/assets/images/constant.png)

So notice the running time of a constant operation regardless of the input size. We can have an array of a million elements. It's going to run the same as an array that has you know just one element. It's just immediately going to return the data because we have the index position of where we want.

<h1 id="4. Quadratic growth rate">4. Quadratic growth rate</h1>

Let's look at an algorithm that would be much slower than the one we have here. And that is a loop that's inside of a loop. And when we have loops inside of loops things really start to slow down. For example, take a look at this method:

{% highlight java %}
public int countDuplicate(int items1[], int items2[]){
    int count = 0;
    for(int i = 0; i <= items1.length; i++){
        for(int j = 0; j < items2.length; j++){
            if(items1[i] == items2[j]){
                count++;
            }
        }
    } return count;
}
{% endhighlight %}

This method is supposed to count the number of integers that exist in both of the arrays that are passed as input to this method. `Items 1` and `items 2` are the arrays, and the way it does this is by comparing each element in one array with every element in the other. So you can imagine that this kind of thing is not going to scale as well as the linear one we saw before. But then of course it solves a different kind of problem.

Now let's say if the first array contains 10 elements and the second array also contains 10 elements that would result in 10 times 10 100 iterations. But if we have 100 elements in the first array and a hundred elements in the second array that jumps to 100 times 100, i.e. 10000 operations. Now if the first array contains a thousand elements and so does the Second we're talking about a whopping million operations or a million iterations. So clearly this method is not as scalable as the previous one. We looked at the number of operations that will need to be run will be equal to the size of the input squared.

So if I wanted to graph the running time of this method the graph would look roughly something like this: 

![image quadratic](https://raw.githubusercontent.com/Damans227/BlogV1/gh-pages/assets/images/quadratic.png)

As you can see this does not scale as well with large inputs. The more input values we run in the algorithm, the slower it's going to get. And there's kind of a structure that has to iterate over a loop that is inside another loop is referred to as a `quadratic`. The term quadratic in math simply means squared and the number of operations the computer will run in this kind of an algorithm is going to be the `input squared`. That's why it's referred to as a `quadratic`.

<blockquote>So keep these terms in mind, we got linear, constant and we have quadratic and don't let these fancy mathematical terms scare you.</blockquote>

<h1 id="5. Big O notation">5. Big O notation</h1>

When we talk about terms like linear, quadratic we're basically communicating in English. But to communicate these kinds of ideas globally you need in a language that transcends all countries and cultures. So there's no confusion. And in most sciences this is done through symbols and notations and computer science is no different to communicate the efficiency of algorithms. We use a shorthand notation called asymptotic notation.

When we talk about an algorithm that scales linearly we write this `"O(n)"` and this is pronounced Big-O of n, a quadratic growth rate algorithm would be written like this `"O(n<sup>2</sup>)"`  Big-O of n square and “n” here is considered the input size or the number of elements that were given to this algorithm to process. And this notation or equation you can call it represents the growth rate of the algorithm. In other words how well this algorithm scales relative to the size of the input. That's all you really need to be concerned about.

Now we are not completely through with algorithm analysis and big notation. There's just a little bit more theory we need to talk about another genre of problems that scale logarithmically but I'll leave that for later. We will be revisiting this for a brief period of time a little, So stay tuned and I'll see in the next blog!
