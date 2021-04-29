---
title: "Jocular Java Facts - 2/24/21"
published: true
---

Hello and welcome to the inaugural release of Aj’s Joculuar Java facts, so called because it’s alliterative, not necessarily because it’s funny.

What do you think is the result of `Math.abs(-2147483648)` ? No, it’s not actually `2147483648`, it’s `-2147483648`!!! This is the only negative integer for which Math.abs does not return a positive, and it’s because of twos’ complement and 0. The short version is, twos’ compliment is the most common way that computers store negative numbers, and because it makes use of every bit, while not wasting any, and because it needs a way to represent 0, there actually ends up being one more negative than there are positives. This is why the max integer is `2147483647` but the minimum integer is `-2147483648`! And because `2147483648` doesn’t fit in an integer (it’s one bigger than the max), the designers had to make a choice: either `Math.abs(int)` has to return a `long` or bigger, or the minimum integer has to be treated differently. 

There is actually a way of representing negative numbers that is less common called ones’ compliment. It doesn’t have this problem, because the number of positive and negative numbers are the same. The downside? It has two 0s, positive and negative 😱.
