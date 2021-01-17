---
title: "Always make your constructor private when using value object"
date: "2020-06-03"
categories: 
  - "web"
tags: 
  - "dx"
  - "named-constructor"
  - "oop"
  - "php"
  - "value-object"
---

Every PHP developer has learned that to instantiate an object since PHP5 one should use PHP's magic method `__construct`. But what most developers do not realise is that for a better DX usage, using by default this magic method should be avoided if what you are about to instantiate is not a service but an entity, a data transfer object or a value object.

## In the beginning

For the purpose of this article we will work with a putative `Example\Geolocation` object but it could be whatever you want as long as it is a value object.

Intuitively if you need to create such object you will write the following code

\[gist id="365b6e4f435c1c844099aeb7b2f3fa18" file="geolocation-basic.php"\]

As you can see the fully typed class and its constructor are straightforward. However, this is where the devil starts to show its evil head. While this object will fully do what you expect it to do, you still need to validate the coordinates to be sure that on instantiation the object is valid.

You will want to:

- create a `filterLatitude` private method to make sure:
    - the latitude value does not exceed the -90 and +90 range value
    - of if it does you capped that value
- create a `filterLongitude` private method to make sure:
    - the longitude value does not exceed the -180 and +180 range value
    - of if it does you wrapped that value

Which means that your constructor becomes something along this line:

\[gist id="365b6e4f435c1c844099aeb7b2f3fa18" file="geolocation-validation.php"\]

## Then came unexpected constraints

But then, business comes to you and says that they will get the coordinates in form of degrees and decimal minutes. You have 2 choices, you either create a second class which use degrees, an interface to interact with the current object and a full test suite to the make your developer life more miserable or you can add a named constructor to your object.

For those who do not know what a named constructor is, it is a public static method designed as a small factory to create a new instance of the object to which it is attached to. It is PHP substitution to method overloading which does not exist in PHP.

In our example in means that you end up with something along this line:

\[gist id="365b6e4f435c1c844099aeb7b2f3fa18" file="geolocation-from-ddm.php"\]

## Decoupling object instantiation from object usage.

Everything works, and you are happy about yourself. However now you effectively have two ways to instantiate your object and none can take precedence above the other to be declare as the one and only true way to instantiate your object.

As a matter of fact from an outsider point of view, he/she do not care how the object is declare as long as it is valid. The only solution to this is to again rewrite the class as follow:

\[gist id="365b6e4f435c1c844099aeb7b2f3fa18" file="geolocation-final.php"\]

So now we have an object with a better DX

\[gist id="365b6e4f435c1c844099aeb7b2f3fa18" file="geolocation-dx.php"\]

and with the following added values to named but a few:

- Both calls can generate a valid `Geolocation` object which is self validated and simpler to reason with.
- You removed from public API the ability to being able to call twice the constructor (unless you start using reflection).
- Your object is extensible enough to be able to be instantiate with meaningful name by supporting other named constructors.

For instance, you can easily add more named constructor depending on new business requirements without having to refactor your application core.

\[gist id="365b6e4f435c1c844099aeb7b2f3fa18" file="more-named-constructor.php"\]

## Known pitfalls

Named constructors should never be generics. I often see named constructor called `create` or `make` with too much business logic behind them. If we use our `Geolocation` example, the following is a bad use of the named constructor.

\[gist id="365b6e4f435c1c844099aeb7b2f3fa18" file="named-constructor-too-generic.php"\]

Behind the scene the `make` method tries other named constructors until it finds the "correct one" or fails. The problem with this sort of construction is that it is difficult to reason with it and it may lead to false positive passing through your tests and business requirements. Your intent should be as clear as your named constructor.

Another pitfall is to make the static named constructor arguments to broad.

\[gist id="365b6e4f435c1c844099aeb7b2f3fa18" file="variable-too-broad.php"\]

The `RequestInterface` has too many properties that it is virtually impossible to know which value is effectively used.

A better solution would be to use:

\[gist id="365b6e4f435c1c844099aeb7b2f3fa18" file="narrow-variable.php"\]

I have purposely left the request body parsing outside of the method which means that nothing can now prevent you from using the same named constructor from a `Symfony\HttpFoundation\Request` object.

## TL;DR

Whenever you can please favour named constructor usage and mark PHP default constructor as inaccessible from the public API. While it may at first seems odd or perceived as adding more constraints. It effectively makes your code more flexible and reduce the complexity of your object usage.
