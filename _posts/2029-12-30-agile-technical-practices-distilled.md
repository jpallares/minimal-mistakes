---
title: Book - Agile Technical Practices Distilled
tags: [technical, book, agile, practices]
excerpt: A technical book that forces you to practice what you learn.
lang: en
---

I try to read technical books often, the problem for me is I like to practice while reading so I really learn it. Some books I started in the past I stopped them because I didn't have the time or the chance to practice what I was reading.

The book [Agile Technical Practices Distilled](https://www.amazon.es/Agile-Technical-Practices-Distilled-principles-ebook/dp/B07TWBZX82/ref=sr_1_2?__mk_es_ES=%C3%85M%C3%85%C5%BD%C3%95%C3%91&dchild=1&keywords=agile+practices+distilled&qid=1587904671&sr=8-2) is great because of that, every chapter has katas or any other tasks to practice what you learnt and I'm loving it.

I'm uploding the katas to a [Gitlab repo](https://gitlab.com/agile-practices-distilled) and for some months, we had a **book club** at the company I work for. We went through the different implementation of the katas that everyone did. It was really useful to see others points of view and debating why someone took that decision or the other.

Some of the discussions/learnings I had during this kata analysis:

- Stats counter

  - What output format shall we use?
  - Better counting so no need to count at the end? More performant?

- Anagram

  - Hard effort to chose test input aa aaa until I used Set

- Roman numerals

  - I used to do while too early (after seeing a bucnh of ifs) with the [TPP (Transformation Priority Premise)](https://en.wikipedia.org/wiki/Transformation_Priority_Premise) I started looking for tail recursion.

- TicTac I

  - Can we ignore the chip an alternate automatically?

- TicTac II

  - Better linq complex that nested loop?
  - Too big panel class?
  - Current chip to say who wins?

- GameOfLife

  - Nested loop or int as parameter or class just for int?

- Tennis

  - Refactor following calisthenics pointed to an Score class and maybe even more? WorthIt?
  - Dictionary<string,int> for player score?

- Refactor smelly tic tac toe
  - When to stop?
  - Class por position X Y?
  - Create tile as parameter? We break tests

After Christmas break the book club ended but during this pandemic I resumed reading the book and I'm uploading again the katas to the repo. Are you currently reading any technical book? Do you by chance implemente any any of the katas? Let's discuss!
