---
title: Complete-Me
---

## What is a trie?

A trie is a data structure in computer science. The word trie is derived from the word retrieval (as in re-`trie`-val).

Now there are many types of tries and one you will hear a lot about is the `binary search trie`. It is similar to a linked list the difference being that each child node has a single left and right node attached to it.

The benefits of something like a `trie` is that it makes dealing with large sets of data easier to handle.

## What do you mean by data structure?

A data structure is just a particular way of organizing data so that it can be accessed and modified efficiently and quickly. Up to this point you've used data structures that are built into javascript to manage how your data is accessed and manipulated (Array and Object). 

Although Arrays and Objects are great for smaller sets of data it becomes a lot more difficult to manage 

Consider the following gif.

![](https://i.gyazo.com/77f415128f0ea9ae46b80a61a127d9dc.gif)

If we structure our data in such a way that it becomes easier to access we can rule out data that doesn't have to be sifted through or looked at. This makes queuing our data set more performant, predictable, and manageable. 

## Let's talk about a prefix trie

A prefix trie is comprised of nodes. The distinguishing factor of the prefix trie is that every node will house every possible solution. In our case that means a child node can have up to 26 children (every letter of the alphabet).

Here's an arbitrary example of what a potential prefix tree could look like if you were storing names. 

           [ root ]
            /     \
           .       .
          /         \
         [a]        [e]
        /   \       /  \
      [m . . n]   [m  . z]
       |     |     |    |
      [y]   [n]   [m]  [r]  
             |     |    |   
            [a]   [a]  [a]  
          /  |  \      
        [b . i . l]
         |   |   |
        [e] [k] [i]
         |   |   |
        [l] [a] [s]
         |       |
        [l]     [a]  
         |
        [e]

In our example here we have two parent nodes. `a` and `e` they have children nodes of `m`, `n`, `m`, `z`. It continues to trickle down until we get to a completed name.
If we query the trie for names that begin with `a` our data set is sizably reduced because we can ignore any name that doesn't start with an `a`. Thus making our response time faster and more predictable. 

## Complete Me

Autocomplete features are a very common convention for text inputs on search fields. In this project you are going to be building a low level version of an auto complete system in JavaScript. You'll use the boilerplate repos you created during the project configuration lesson by following these steps:

1. Retrieve the git remote URL for your boilerplate repo by navigating to your repo at github.com. It should be something like `https://github.com/brittanystoroz/boilerplate.git`. Copy this to your clipboard.

2. In your terminal, create a new project directory called `complete-me`. CD into it and run `git init`

3. Add your boilerplate repo as a remote called `boilerplate` with the following command:

`git remote add boilerplate https://github.com/brittanystoroz/boilerplate.git`

4. Copy your `boilerplate` master into your `complete-me` master with the following command:

`git pull boilerplate master`

5. Go back to github in the browser and create a new repository called `complete-me`. Do **not** add a `.gitignore` file and do **not** add a license.

6. Click the 'Create Repository' button and copy the git URL for your new repo to your clipboard. It should be something like `https://github.com/brittanystoroz/complete-me.git`

7. In your terminal, in your `complete-me` directory, add your new github repo as a remote with the following command:

`git remote add origin https://github.com/brittanystoroz/complete-me.git`

8. Push up your current master branch to your origin remote:

`git push origin master`



### Hint
You can use `console.log` along with `JSON.stringify` to view your trie in your console when running your tests.
`console.log(JSON.stringify(trie, null, 4))`

## Requirements

## Phase 1

The first thing your `trie` should be able to do is take in a word. It should also keep a count of how many words have been inserted.

```js
import Trie from "./lib/Trie";

var prefixTrie = new Trie();

prefixTrie.insert("hello");

prefixTrie.count();
=> 1

prefixTrie.insert('world');

prefixTrie.count();
=> 2
```

## Phase 2

Once the words are placed into the `trie` it should be able to offer some suggestions based on a word prefix. 

You will need to write a method called `suggest` that will take in a word prefix and return an array of words that match the desired prefix. 

```js
prefixTrie.suggest('he');
=> ['hello']

prefixTrie.insert("hellen");

prefixTrie.suggest("he");
=> ["hello", "hellen"]

prefixTrie.suggest('w');
=> ["world"]
```

## Phase 3

Our Trie won't be very useful without a good dataset to populate it. Our computers ship with a special file containing a list of standard dictionary words.

It lives at `/usr/share/dict/words`

Using the unix utility `wc` (word count), we can see that the file contains 234371 words:

```
$ cat /usr/share/dict/words | wc -l
=> 234371
```

Our next objective is to load the dictionary into our trie. It should have a method called `populate` that will take in the desired data set and inject it into our trie.

```js
import fs from 'fs';

const text = "/usr/share/dict/words";
const dictionary = fs.readFileSync(text).toString().trim().split('\n');

const prefixTrie = new Trie();

prefixTrie.populate(dictionary);

prefixTrie.count();
=> 234371

prefixTrie.suggest('world');
=> [ 'world', 'worlded', 'worldful', 'worldish', ...]
```

## Phase 4 (not due upon evals)

Next week you will create a Weather App that needs an autocomplete feature.
Package your complete-me trie in a node module so that you can import it into
future projects. (Note: don't publish to npm, you can install your package from github)

## Extensions

### Front Facing Application

See if you can implement a front facing application for your `trie`. The user should be able to submit a word and then receive the suggestions on the DOM.

### Delete method

Sometimes auto-completes give suggestions which we never want to see. Add a delete method to your Trie. 

```js
prefixTrie.suggest('world')
=> ['world', 'worlded', 'worldful', 'worldish', ...]

prefixTrie.delete('worldful');

prefixTrie.suggest('world')
=> ['world', 'worlded','worldish', ...]

```

## Evaluation Rubric

The project evaluation will have two parts: 
* an in-person live code/whiteboarding session
  - be able to whiteboard/draw out how methods like insert or find would work in the trie 
  - implement a new method, and/or remove and re-implement a pre-existing method
  - demonstrate your problem-solving process
* submission of the complete project
  - complete functionality
  - complete testing suite
  - instructors will do code reviews

Complete Me will be assessed with the following rubric:

### 1. Process

* 4: Developer demonstrates a clear understanding of their own problem solving process. Logically breaks down large problems into manageable challenges. Has a thoughtful, refined strategy for approaching complex challenges. Developer clearly articulates thought processes.
* 3: Developer has strategies for approaching complex challenges. Can explain thought process and strategy when prompted. 
* 2: Developer demonstrates a haphazard, trial and error approach, without clear strategy. Developer does not articulate thought process clearly, and cannot explain the problem-solving strategies they utilized.
* 1: Developer does not demonstrate any strategy or process. No meaningful code is written and developer cannot articulate their process.

### 2. Fundamental JavaScript & Style

* 4:  Application demonstrates excellent knowledge of JavaScript syntax, style, and refactoring
* 3:  Application shows strong effort towards organization, content, and refactoring
* 2:  Application runs but the code has long methods, unnecessary or poorly named variables, and needs significant refactoring
* 1:  Application generates syntax error or crashes during execution

### 3. Test-Driven Development & Code Sanitation

* 4: Application is broken into components which are well tested in both isolation and integration using appropriate data. Linting shows 0 complaints.
* 3: Application is well tested but does not balance isolation and integration tests, using only the data necessary to test the functionality. Linting shows five or fewer complaints.
* 2: Application makes some use of tests, but the coverage is insufficient. Linting shows ten or fewer complaints.
* 1: Application does not demonstrate strong use of TDD. Linting shows more than ten complaints.

### 4. Functional Expectations

* 4: Application meets all requirements, and implements one extension properly.
* 3: Application meets all requirements as laid out per the specification.
* 2: Application runs, but does not work properly, or does not meet specifications.
* 1: Application does not run, crashes on start.


## Additional Resources

Take a moment and read more about Tries:

* [Tries writeup in the DSA Repo](https://github.com/turingschool/data_structures_and_algorithms/tree/master/tries)
* [Tries Wikipedia Article](https://en.wikipedia.org/wiki/Trie)


If you would like to watch an informative video on tries:

* [Tries Video](https://www.youtube.com/watch?v=zIjfhVPRZCg)
