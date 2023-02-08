---
title: 'Things to Know When Programming in Oop'
date: 2022-09-16T08:52:59+05:30
draft: true
---

# Things to keep in mind

1. Read the problem statement correctly
2. Think in the domain
3. Use constants instead of magic numbers
4. Avoid using primitives
5. Law of demeter ( don't talk to friends of friends )
6. Avoid using static methods
7. Tell don't ask rule
8. Structuring tests i.e. arrangement, action and assertion (3A rule)
9. Have richer exceptions i.e. capture data in the exceptions. Suffix exception classes with `Exception`
10. Use `this` to invoke method in a method if it is taking argument of the same type
11. Insist on having conversation
12. YAGNI rule for example don't use inheritance/interfaces until these are needed
13. Isolate the problem
14. Start with the test as it drives from the usages
15. Avoid type casting
16. Prefer using factory method to create class instances
17. Prefer strict equality (don't override `equals` for the domain. Create new method to do same)

18. Refactor things when you see them instead of waiting for last.
