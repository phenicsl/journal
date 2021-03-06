 Python Notes
==============

DSU Idiom
---------

DSU idiom is so named as Decorate-Sort-Undecorate after its three steps:
- First, the initial list is decorated with new values that control the sort
  order.
- Second, the decorated list is sorted.
- Finally, the decorations are removed, creating a list that contains only
  the initial values in the new order.


bisect
------

There are two bisect methods in bisect module:
- bisect_left
- bisect_right

According to the manual:
- `bisect_left`, If item is already present in list, the insertion point will
   be before (to the left of) any existing entries.

- `bisect_right`, will return an insertion point which comes after (to the
   right of) any existing entries of item in list.

So, what exactly does this mean? Let's put it in a much simple way. 

- `bisect_left`, if item "y" is present, then it will return the index of the
   first "y" in the sequence.

- `bisect_right`, if item "y" is present, then it will return the index of the
   first item "x" that has "x > y".

metaprogramming
---------------

Classes are also objects in python, creation and initialization of classes are
controlled by metaclass in python. In one hand, python treat classes as if they
are normal objects, but in another hand, classes also have some special meaning
other than objects.

__new__ and __init__
~~~~~~~~~~~~~~~~~~~~

As objects, classes are created and initialized by `__new__` and `__init__`
methods defined in its metaclass. The difference is that when those two methods
are called, they are passed in with predefined sepcial parameters::

  class Meta(type):
      def __new__(metacls, name, bases, dict):
          type.__new__(metacls, name, bases, dict)
  
      def __init__(cls, name, bases, dict):
          type.__init__(cls, name, bases, dict)

The first parameters be passed to `__new__` and `__init__` are different,
`__new__` takes the metaclass itself as the first parameter, but `__init__`
takes the reference to class object that was created as the first parameter. It
is the same as ordinary classes definition, in an ordinary class definition,
`__new__` takes the first parameter to be the class itself, but `__init__` takes
the objected to be created as first parameter.
    

__call__
~~~~~~~~

We created a object by actually calling the Class, so as usual callable
object invocation, we actually calling the metaclass's `__call__`
method. For example::

    var = Some_Class(foo, bar)

    # is actully 

    var = Meta.__call__(Some_Class, foo, bar)

This `__call__` is defined in metaclass of that class and will call class's
`__new__` and `__init__` by default as following example::
    
  class Meta(type):
      def __call__(cls, *args, **kwargs):
          instance = cls.__new__(cls, *args, **kwargs)
          if instance:
              cls.__init__(instance, *args, **kwargs)


How to call super __new__ and __init__ in metaclass
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`__new__` is a implicit static method, which means you nerver decorate it with
the `@staticmethod` decorator. `__init__` is a instance method. When we define
those two method, most of the time, we may need to call corresponding method in
super class firstly.

`__new__` and `__init__` is defined with following prototype::

    class Meta(type):
        def __new__(metacls,              # metaclass itself
                    name,                 # name of the class to define
                    bases,                # base class tuple
                    dict)                 # class object dict
      
        def __init__(cls,                 # class object, just like self in object definition
                     name,                # name of the class
                     bases,               # base class tuple
                     dict)                # class object dict

Since `__new__` is static method and the first parameter is actully the
parameter,


Package, Module and Import
--------------------------
when import from a package or module, `from XXX import YYY` statement also
will be executed. Then YYY will actually become one variable inside the
imported module, and could be accessed via `module.YYY`. For example::


   # module argvs
   from sys import argv

   # module test
   import argvs
   
   # argv could be accessed with argvs.argv
   print argvs.argv     # => []


When import a pacakge with `import package` or `from pacakge import XXX`, we
actually will execute `package/__init__.py` firstly, so most of the time, we
will import all necessary package-scope variables from submodules in the
`__init__.py` and make them to be package-scope variables.

Another worth-mentioned feature is that when execute `from XXX import *`,
python actually will check `XXX.__all__` firstly to see if programmer has
restricted all variables that could be imported. So a best here I can suggest
is that define `__all__` attribute inside each submodules inside a package
and use `from submodule import *` in the `__init__.py` file, that way, we may
restrict the definition of package-scop public variables in different
submodules. 

Cookbook
--------

How to install python packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Install python-setuptools firstly, then use easy_install to install packages
listed on http://pypi.python.org. For example, if you want to instlal multitask,
then use the command below::

   easy_install multitask

easy_install will download and intall the package, dependences will be solved
automatically.



How to use sphinx and autodocument?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Install sphinx with command::

      easy_install sphinx

2. Make a initialize configuration with::

    sphinx-quitstart

It will ask several questions about the configuration, generate the
configuration file and also will generate the Makefile.

3. Make sure the package you are going to auto document is in the PYTHONPATH.

4. Generate document by Makefile::

    make html

will generate html output.


