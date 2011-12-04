Scala Document
==============

Scala method definition
-----------------------
Scala method definition follows following format ::

    def MethodName(param: ParamType) : ReturnType = {
       ...
       // method body
       ...
    }

- if method has only a single result expression, then you may can leave off the
  curly braces ::
    
    def MethodName(param: ParamType) : ReturnType = // method body

- if method has a return type to be Unit, then you may omit the ``ReturnType``
  and ``equal sign`` ::
    
    def MethodName(param: ParamType) {
      ...
      // method body
      ...
    }

If you omit the equal sign of a method definition, then the return type will
definitely be ``Unit``. If the return type of a method is declared to be
``Unit``, then any value returned from it will be converted to be ``Unit``.

The rules of semicolon inference
--------------------------------
1. The line question ends in word that would not be legal as the end of a
   statement, such as a period or an infix operator

2. The next line begins with a word that cannot start a statement

3. The line ends while inside parentheses (...) or brackets [ ... ].


Operator
--------
 
In Scala, operators are not special language syntax: any methods can be an
operator. What makes a method an operator is how you use it. when you write
``s.indexOf('o')``, then it is not a operator. But when you write ``s indexOf
'o'``, then it is a operator.

Identifier
----------

alphanumeric identifier
~~~~~~~~~~~~~~~~~~~~~~~
An ``alphanumeric identifier`` starts with  a letter or underscore, which can be
followed by further letters, digits, or underscore. 

operator identifier
~~~~~~~~~~~~~~~~~~~
An operator identifier consist of one or more operator characters.

mixed identifier
~~~~~~~~~~~~~~~~
A mixed identifier consists of an alphanumeric operator, which is followed by an
underscore and an operator identifier.

literal identifier
~~~~~~~~~~~~~~~~~~
A literal identifier is an arbitrary string enclosed in back literals (`...`). 

Traits
------
Stackable
~~~~~~~~~
When mulitple traits are mixed into a class, the order of mixins are
significant. Traits futher to the right take effect first. When you call a
method on a class with mixins, the method in the trait furthest to the right is
called first. If that method calls super, it invokes the method in the next
trait to its left, and so on.

With traits, the method called with `super` is determined by a linearization of
the classes and traits that are mixed into a class. When you instantiate a class
with `new`, scala takes the class and all of its inherited classes and traits
and puts them into a single, linear order. Then, whenever you call super inside
one of those classes, then invoked method is the next one up the chain. 

Package Object
--------------
Each package is allowed to have one package object. Any definitions placed in a
package object are considered members of the package itself.

Case Class
----------
When use the modifier `case class`, scala compiler will add some syntactic
convenience to your class:
1. It adds a factory method with the name of the class.
2. All arguments in the parameter list of a case class implicitly get a val
   prfix, so they are maintained as fields
3. The compiler adds "natural" implementations of methods `toString`,
   `hashCode`, and `equals` to your class.
4. The compiler adds a `copy` method to your class for making modified copies.

Pattern Matching
----------------
Kinds of Patterns
~~~~~~~~~~~~~~~~~
* Wildcard patterns
  The wildcard pattern (_) matches any object whatsoever
* Constant Patterns
  A constant pattern matches only itself.
* Variable Pattern
  A variable pattern matches any object, just like a wildcard. Unlike a
  wildcard, Scala binds the variable to whatever the object is.

  Scala uses a simple to distinguish between `variable pattern` and `constant
  pattern`. A simple name starting with a lowercase lettern is taken to be a
  pattern variable; all other references are taken to be constants.

* Constructor Pattern
  Assuming the name designates a case class, such a pattern means to first check
  that the object is a member of the named case class, and then to check that
  the constructor paramters of the object match the extra pattern supplied. 

  *Deep Match* is supported in Scala, such patterns not only check the top-level
  object supplied, but also check the contents of the object against further
  patterns.

* Sequence Pattern
  
* Tuple Pattern
 
* Typed Pattern
  
Pattern Guard
~~~~~~~~~~~~~
A pattern guard comes after a pattern and starts with an if. The guard can ben
an arbitrary boolean expression, which typically refers to variables in the
pattern. If a pattern guard is present, the match succeeds only if the guard
evaluates to true.



