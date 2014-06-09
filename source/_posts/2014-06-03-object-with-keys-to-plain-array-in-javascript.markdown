---
layout: post
title: "Object with keys to plain array in Javascript"
date: 2014-06-03 15:56:07 +0100
comments: true
categories:
- Javascript
---

Something which quite a few people, especially people new to Javascript have a problem with, is itterating over an Object.

By Object I mean, an Object which has keys, which contain values. How do you itterate over the Object and access the data in each key of the Object. With an array this would be easy, but how do you treat an Object like an Array.
<!-- more -->

There are a few ways to solve this problem, but to illustrate the problem and solution, lets make up a scenario. Lets say we have a zoo, like "Billys Zoo".

Billy might want to know what animals he has, he would want to know what type of animals he has, aswell as the individual breeds.

So if he was to store this in Javascript, he might have something like this:

{% gist d0c85ccd4c02b9b8bc68 object_to_array_animals.js %}

Which is great, he knows what types of animals he has, and what breeds.

What if he wanted to display all of the different breeds of *animals* he had on his fictitios website, he would need a way to itterate over his *object* which contains all the animals.

So he needs a way to produce an *array* of all of the different breeds he has. I recently had to do something similar to this, and sometimes newbies to javascript have trouble itterating with Objects. These are two simple ways to achieve this:

## Method one - For loops

{% gist d0c85ccd4c02b9b8bc68 object_to_array_animals_first.js %}

As you can see, this is quite a bit of code, to do something simple. It required you to have two for loops with seperate counters in each, then to manually push the breeds into the array.

## Method 2 - Array#forEach
*This method uses Ecmascript5 methods so make sure you know that or you will wonder why its not working*

The second method uses [Object#keys](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys), [Array#forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) and [Array#concat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) which make the code a bit more natural and less error prone.

{% gist d0c85ccd4c02b9b8bc68 object_to_array_animals_second.js %}

`Object.keys()` will get the different keys of an Object and turn it into an array.  
Then with this array we can use `Array.forEach()` to itterate over the keys, so inside the forEach, `animalType` is a reference to the `animals` keys (dogs, lizards).

With this we can then access the animalBreeds by using bracket notation `animals[animalType]`.  
`Array.concat()` can be used to join array values together, so we can pass the `animals[animalType]` to join the animal breeds together. `Array#Concat` returns a new array based on the two array which are joined, so then we simply assign this return value to the `animalBreeds` which makes it append the breeds.

## Bonus Snippet

As a Bonus snippet, its also really easy to be able to turn the `animals` into multidmentional array which contains the breeds.

{% gist d0c85ccd4c02b9b8bc68 object_to_array_animals_bonus.js %}

This effectively removes the `keys` (they are actually there 0..1 etc) from Object, and turns it into an array instead. Which then can be itterated easier. Depending on how you want the data structured, this could be a better data structure.

The [Array#map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) function executes a callback on every element of an array and then creates a new array from the results.

So we use `Object.keys()` to get the object keys, then we return the animal breeds arrays, which will create the array containing each array of animal breeds. Really easy, really simple.
