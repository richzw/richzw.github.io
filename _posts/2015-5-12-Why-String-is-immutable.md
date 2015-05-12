---
layout: post
title: Why String is immutable
---

**Question**: [Why String is immutable in Java?](http://stackoverflow.com/questions/22397861/why-is-string-immutable-in-java)


`String` is immutable for several reasons, here is a summary:

- **Synchronization**: making String immutable automatically makes them thread safe thereby solving the synchronization issues.

- **Caching**: when compiler optimizes your String objects, it sees that if two objects have same value (a="test", and b="test") 
and thus you need only one string object (for both a and b, these two will point to the same object).

- **Class loading**: String is used as arguments for class loading. If mutable, it could result in wrong class being loaded
(because mutable objects change their state).

- **Efficiency** The hashcode of string is frequently used in Java. For example, in a HashMap. Being immutable guarantees that
hashcode will always the same, so that it can be cached without worrying the changes.That means, 
there is no need to calculate hashcode every time it is used.

- **Security**: parameters are typically represented as String in network connections, database connection urls,
usernames/passwords etc. If it were mutable, these parameters could be easily changed. 
[Time of check to time of use](http://en.wikipedia.org/wiki/Time_of_check_to_time_of_use) is one good example to explain it.

