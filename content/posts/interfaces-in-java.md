---
title: 'Interfaces in Java'
date: 2022-09-07T12:39:26+05:30
draft: false
tags:
  - java
---

In java, whenever you pass some value to some function, the type of value that you pass to that function defines the contract. As long as your the values satisfies the contract you are good to go.

`Interface` is good example of it. Interaface can be created to enforce some contract.

Let's take example of payment using some payment instrument like credit card, debit card or net banking.

What contract these all should satisfy so that amount can withdrawn from these. It can be that amount should be debitable. As long as all these satisfy debitable contract they can be used for withdrawing money.

Method which takes these performs this transaction can take one type of value, that value denotes that it will satisfy contract of debit. It doesn't matter what all contract it satisfy but as long as it satisfy contract of debitable.

Here comes idea of interface, all the payment instrument that can be used to pay the amount can implement interface, let's call it `Debitable`. Method which performs debit action can collect payment instrument as type of that `Debitable`. So only debit method which is enforced by `Debitable` is accessible.

> Interaface are contracts, enforcing all who implements it to satisfy the contract.
>
> > Type can be thought as contract.

# References

[Interface Defination](https://docs.oracle.com/javase/tutorial/java/concepts/interface.html)
[Interfaces Oracle docs](https://docs.oracle.com/javase/tutorial/java/IandI/createinterface.html)
