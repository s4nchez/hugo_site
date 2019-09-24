---
layout: post
title: "Diamond Kata using Clojure and TDD"
date: 2014-12-06T21:00:00+01:00
---
After seeing [Ron Jeffries' post](http://ronjeffries.com/articles/diamond3/three-of-diamonds.html) about different takes on the Diamond Kata, I've decided to try it as well.

This comment on [Philip Schwarz' solution](https://github.com/philipschwarz/diamond-problem-in-clojure) in particular got my attention:

> I don’t know Clojure, which certainly made Philip’s solution harder to grok, but one can sort of read it. He added some tests later, which certainly helps.

Would a solution driven by tests be easier to understand? I'll let you be the judge. Check out [my solution on GitHub](https://github.com/s4nchez/diamond-kata-clojure-tdd) now, or keep reading for a detailed description (spoilers) of how I got to it.

## My solution step-by-step

To avoid spoiling my take on it, I decided not to read other solutions beforehand. I used [Seb Rose's initial article](http://claysnow.co.uk/recycling-tests-in-tdd/) as a reference and tried to start with the simplest test I could think of:

```clojure
(deftest diamond-building
  (testing "Diamond for A"
    (is (= '("A") (diamond "A")))))
```

Followed by a fake implementation:

```clojure
(defn diamond [letter] '("A"))
```

So with my initial test passing I tried to jump to something a bit more meaningful like:

```clojure
(testing "Diamond for B"
    (is (= '("-A-", "B-B", "-A-") (diamond "B"))))
```

And that was enough to get me stuck! I felt overwhelmed by the amount of complexity that the proper solution for the second test required and saw myself forced to step back and try to break the problem into smaller parts that I could fit into my head.

To decide how to split the problem, I've looked at another example, the diamond for ```C```:

```
--A--
-B-B-
C---C
-B-B-
--A--
```

I noticed I could try to tackle a few parts of the problem independently:

1. The amount of spaces outside the diamond for each letter
2. The amount of spaces inside the diamond for each letter
3. Putting a line of the diamond together
4. The letter sequence to compose the rows diamond

I've decided to start with #2 because it looked simpler than #1: the inner part of the diamond does not depend on the size of the diamond itself (e.g. ```B-B``` and ```C---C``` will always have the same amount of spaces inside).

### The inner part of the diamond

It also happens that the number of spaces inside the diamond follow a simple formula: ```(2 * n) - 1```, where ```n``` is the index of the letter in the diamond. The only exception is the letter ```A``` that doesn't contain any space and is not repeated on its line.

So I've parked my initial tests and wrote a new one to help me implement just the inner part of a line:

```clojure
(deftest inner-part-building  
  (testing "A"
    (is (= "A" (inner-part "A"))))
```

That was easy enough to fake as well:

```clojure
(defn inner-part [letter] "A")
```

So again, I've added a few more test cases:

```clojure
(deftest inner-part-building
  (testing "A"
    (is (= "A" (inner-part "A"))))
  (testing "B"
    (is (= "B-B" (inner-part "B")))))
```

Then I could start splitting the logic for ```A``` and the other letters by introducing a conditional:

```clojure
(defn inner-part [letter]
  (cond (= "A" letter) letter
        :else "B-B")
```

At this point I decided to replace the ```B-B``` from my solution by the actual implementation. 

So I added the test case for ```C``` and realised I still didn't have a function to give me the index of a particular letter (```A -> 0```, ```B -> 1```, ```C -> 2``` and so on) to use in the formula mentioned above. 

After a few more red-green cycles (which I'll omit from now on as it gets boring really quickly), I've ended up with this two functions:

```clojure
(defn char-index [letter] (- (int (first (char-array letter))) 65))

(defn inner-part [letter]
  (let [index (char-index letter)]
    (cond (= 0 index) letter
          :else (str letter (string/join "" (repeat (- (* 2 index) 1) "-")) letter))))

```

The ```char-index``` function calculates the index of the letter by converting it to int and using the difference from the int value of ```A``` which is 65.

The inner part is then created by concatenating the ```letter``` + ```((2 * n) -1) dashes``` + ```letter```.

### The outer part of the diamond

To calculate the outer part of the diamond I started once more with the simplest case:

```clojure
(deftest outer-part-building
  (testing "A for A diamond"
    (is (= "" (outer-part "A" "A"))))
```

In this case I've used two parameters: one to represent the letter of the line, another one to represent the letter of the diamond. Again, the first implementation was pretty much a stub:

```clojure
(defn outer-part [current-letter diamond-letter] "")

```

Then I've moved to more test cases for the letter ```A```:

```clojure
(deftest outer-part-building
  (testing "A for A diamond"
    (is (= "" (outer-part "A" "A"))))
  (testing "A for B diamond"
    (is (= "-" (outer-part "A" "B"))))
  (testing "A for C diamond"
    (is (= "--" (outer-part "A" "C")))))
 ```

At this point I could tell that the number of spaces depended on the second parameter, so I've implemented it accordingly:

```clojure
(defn outer-part [current-letter diamond-letter]
  (let [final-index (char-index diamond-letter)]
    (string/join "" (repeat final-index "-"))))
```

All the tests were passing but I was pretty sure it wouldn't work for other letters, so I've added another test to show I needed to use the formula ```index of diamond letter - index of current letter``` to figure out the correct number of spaces:

```clojure
(testing "B for F diamond"
    (is (= "----" (outer-part "B" "F"))))
```

Surely enough it failed because my function was just using the diamond index. 

By fixing that I've ended up with the final version of the function:

```clojure
(defn outer-part [current-letter diamond-letter]
  (let [current-index (char-index current-letter)
        final-index (char-index diamond-letter)]
    (string/join "" (repeat (- final-index current-index) "-"))))
```

### Creating the rows

With the basic parts of my solution implemented, now it was time to start putting the pieces together. I've started by the simplest case of single diamond line. The test ended up like:

```clojure
(deftest line-building
  (testing "A for A diamond"
    (is (= "A" (line-for "A" "A"))))
  (testing "A for C diamond"
    (is (= "--A--" (line-for "A" "C"))))
  (testing "C for C diamond"
    (is (= "C---C" (line-for "C" "C")))))
```

And the implementation was very simple:

```clojure
(defn line-for [current-letter diamond-letter]
  (let [outer (outer-part current-letter diamond-letter)
        inner (inner-part current-letter)]
    (str outer inner outer)))
```

### The diamond letter sequence

Now the final big challenge was to create the sequence of the letters for the diamond. I wanted something to produce:

```clojure
(deftest diamond-letters-building
  (testing "A diamond"
    (is (= '("A") (letter-sequence "A"))))
  (testing "D diamond"
    (is (= '("A" "B" "C" "D" "C" "B" "A") (letter-sequence "D")))))
```

Once again the easiest way I could find to achieve that was to use ```char -> int``` conversions, which allowed me to create the following function:

```clojure
(defn letter-sequence [diamond-letter]
  (let [value-a 65
        value-letter (+ value-a (char-index diamond-letter))]
    (map #(str (char %)) (concat (range value-a value-letter) (range value-letter (- value-a 1) -1)))))
```

The result is created by:

  * Creating a first list of ints, from ```A``` up to one letter before the diamond letter (```(range value-a value-letter)``` part)
  * Creating a second list from the diamond letter back to ```A``` (```(range value-letter (- value-a 1) -1))```)
  * Merge the two lists using ```concat```
  * Use ```map``` to convert the ints back to strings.

### Putting everything together

At this stage I could go back to my initial tests:

```clojure
(deftest diamond-building
  (testing "Diamond for A"
    (is (= '("A") (diamond "A"))))
  (testing "Diamond for B"
    (is (= '("-A-", "B-B", "-A-") (diamond "B"))))
  (testing "Diamond for C"
    (is (= '("--A--", "-B-B-", "C---C", "-B-B-", "--A--") (diamond "C"))))

```

The implementation of the ```diamond``` function became trivial:

```clojure
(defn diamond [letter]
  (map #(line-for % letter) (letter-sequence letter)))
```

And that was it. By mapping the ```line-for``` function to each of the letters produced by ```letter-sequence``` I could create the final structure of the diamond.

### Conclusion

Using TDD forced me to realise early on that the problem was not as simple as I thought initially. Using output examples helped me to understand the problem a bit more and breaking it into smaller parts made the red-green-refactor flow very easy.

It was specially fun to see the problem become simpler and simpler as the parts of it were being implemented.

The final solution also became simpler than I expected. Comparing to [Philip's solution](https://github.com/philipschwarz/diamond-problem-in-clojure) it's also required half of his lines of code.

I can't decide if that was just luck on my approach or was a side-effect of TDD. It was definitely not because my Clojure skills, as I'm relatively new to the language.

Overall it was a very fun exercise. Now is time to go back and read how other people have done it.

