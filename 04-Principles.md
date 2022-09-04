# Clean Code Principles

## Classic software failures

* projects go over budget
* companies spend millions and end up nowhere
* bad software causes fatalities, impacts revenue, and can pose generic risks,
  e.g. security incidents

A 2015 article in IEEE spectrum:

* [Transistor Production Has Reached Astronomical Scales](https://spectrum.ieee.org/computing/hardware/transistor-production-has-reached-astronomical-scales)

Every second of 2014, on average 8 trillion transistors were produced. It is
some software that will run on these.

Robert C. Martin motivation: Let us cleanup ourselves before we are going to be
hit by regulation.

We are living in the age of data, so here's a quip on data and code:

> Code ages like fish, data ages like wine.

## Calculating failure costs

* ROI on testing
* How much time can you invest in testing - or improving code in general?

![](static/test_roi.png)

## Clean code layers (top down)

* Architecture
* Patterns
* Data Structures
* Idiomatic Code

### The right architecture and approach

* rarer, but important decisions
* try to postpone hard questions regarding design
* sometimes [Worse is better](https://en.wikipedia.org/wiki/Worse_is_better)

> Worse is better (also called the New Jersey style) is a term conceived by
> Richard P. Gabriel in an essay of the same name to describe the dynamics of
> software acceptance. It refers to the argument that software quality does not
> necessarily increase with functionality: that there is a point where less
> functionality ("worse") is a preferable option ("better") in terms of
> practicality and usability.

### Useful patterns

* code reuse (i.e. find a suitable library)
* tool reuse ("Taco Bell", [article](http://widgetsandshit.com/teddziuba/2010/10/taco-bell-programming.html))

> The more I write code and design systems, the more I understand that many
> times, you can achieve the desired functionality simply with clever
> reconfigurations of the basic Unix tool set. After all, functionality is an
> asset, but code is a liability. [...] Every time you write code or introduce
> third-party services, you are introducing the possibility of failure into
> your system.

* convention over configuration

### The right data structures

* worry about data structures
* rather 1 data structure and 100 methods than 10 with 10 each

### Idiomatic code (readability)

* make code look boring
* make wrong code look wrong
* Perl ("there is more than one way to do it") to Python ("There should be one–
  and preferably only one –obvious way to do it")
* use the language (to your advantage)

### Cross-cutting concern

Worry about things that are not directly code, like deployment, continuous test
and build processes, etc.

* software lifecycle and support
* CI
* testing
* docs (developer, external, ...)
* setup

## Learn from open source projects

* pragmatic
* efficient
* documented

There is plenty wrong with OSS as well, but successful project can be an inspiration.

* Companies switch (or switched) to basically a common open source workflow
  when they adopted hosted git server applications

## SW engineering's greatest hits

* [Software Engineering's Greatest Hits](https://www.youtube.com/watch?v=HrVtA-ue-x0), [Slides](https://third-bit.com/talks/greatest-hits/#1)

What does research says about software development practices?

* novice errors
* TDD studies
* code metrics

> But nothing works better than counting lines of code

* error handling

> Majority of catastrophic failures could easily have been prevented by
> performing simple testing on error handling code

* exceptions

> Most common catch block logs the error rather than trying to recover from it

And the list goes on.

## Good code properties

There are generic ideas and approaches that have been suggested to improve code
quality.

* Question (Pad):

> Name one you would attribute to describe good code and one to less good code

### Design by contract

* Betrand Meyer, 1980s
* Programming language: Eiffel
* deferred PEP-361 (2003): https://peps.python.org/pep-0316/
* https://github.com/Parquery/icontract

Example: [Examples/Contracts]

Without specific contract library:

* makeing properties explicit with assertions or explicit checks (and e.g.
  raising `ValueError` on failures)

### Defensive programming

Design to [...] ensure the continuing function of a piece of software under unforeseen circumstances.

This can mean:

* focus on absence of errors
* readable, auditable code
* extra care when dealing with I/O

#### Error handling

* catch specific errors (avoid empty except)
* handle some gracefully
* fail fast

Find the *right level* for your exception.

* reuse existing exception hierarchy: [https://docs.python.org/3/library/exceptions.html](https://docs.python.org/3/library/exceptions.html)

You can include original exceptions via [PEP-3134](https://peps.python.org/pep-3134/) - "Exception Chaining and Embedded Tracebacks"

> Example: [Example/ExceptionChaining]

> [...] implicit exception context can be supplemented with an explicit cause by using from with `raise`.

#### Use sensible default values

* across various layers
    * command line flags
    * keyword arguments

Use language facilities, like:

```
dict.get(key, default)
```

### Assertions

* `assert`
* assertions as a last resort (e.g. halt program instead of handling an error)

Can be disable at runtime, e.g. with `python -O script.py`

```python
$ python -c "assert False"
Traceback (most recent call last):
  File "<string>", line 1, in <module>
AssertionError
```

With basic optimizations:

```
$ python -Oc "assert False"
```

### Encapsulation

* module interfaces should be simpler than the implementation

In [Philosophy of Software
Design](https://web.stanford.edu/~ouster/cgi-bin/book.php) Ousterhout reports
various issues in implementations:

* students wrote too many classes for the problem - information leakage between
  classes; e.g. two classes to handle HTTP requests - hence both classes
implemented many aspects of understanding the request data structure

> slightly larger classes could have helped to hide information (details about
> the request) better

### Separation of concerns

#### Avoid adding to many responsibilities

Case study: A DSL coupled with a backend storage system (SM).

### Cohesion and coupling

* cohesion: well defined purpose; coupling: dependency between code
* aim for: high cohesion and low coupling ("oss" - separate parts, ...)

### DRY

* don't repeat yourself
* there is also the rule of three - use opportunities to abstract or factor out a piece of code

### YAGNI

* related to TDD a bit
* what you need vs what you want
* some instances: abstracting backends (albeit only one is and will be used)
* any *potential* benefit

> It can be hard to distinguish between design and YAGNI

### KISS

#### from aerospace industry

#### smallest data structure to fit the problem (e.g. graph can be a dictionary)

### EAFP and LBYL

#### python encourages EAFP

### composition and inheritance

#### when to use inheriance -- http package

#### inheritance anti-patterns

#### multiple inheritance and MRO

#### Mixins

#### example for a simple composition, subclass plus mixin

### functions and arguments

#### anything that can be derived should not be passed separately (request)

#### too many arguments lead to higher coupling

#### may group parameters

## coding guidelines

### naming conventions

### reveal your intent

### avoid noise

### class names

### exceptions and exception handling

### variables

## X: improve "ttt" example

## SOLID

### SRP

#### what it says

#### example

### OCP

#### what it says

#### example

### LSP

#### what it says

#### example

### ISP

#### what it says

#### example

### DIP

#### what it says

#### example

## D: give 3 scenarios and ask for the most approriate SOLID principle

## clean architecture

### separation of concerns

### abstractions

## package design

### setup.py

## packaging options

### linkedin example: shiv

### automation with gitlab