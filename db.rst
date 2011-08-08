==================================
DB Notes -- Relationship and NoSQL
==================================

Mongodb
=======

Cookbook
--------

How to create a new database and collection?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To creat a new database, just use it directly, and then when you add any
data, it will be created directly ::
    
    $ mongo
    MongoDB shell version: 1.8.2
    connecting to: test
    > use eservice
    switched to db eservice

To create a colleciton, ``db.createCollection()`` should be used.

How to create index for a collection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a index, use the ``ensureIndex`` method::
    
    > db.people.ensureIndex({'userName': 1})
    
An index need to be created only once for a colleciton, if you try to create the
same index again, then nothing will happen.



