Usage
=====

.. _installation:

Installation
------------

You can find the necessary technologies, packages, libraries and how to install them based on your operating system below:

1) UBUNTU 20.04

1.1) MongoDB Installation

Import the public GPG key

.. code-block:: console

   curl -fsSL https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -
   
create a file in the sources.list.d directory named mongodb-org-4.4.list
.. code-block:: console
   echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 	multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list

update your server’s local package index
.. code-block:: console
	sudo apt update

install MongoDB
.. code-block:: console
	sudo apt install mongodb-org

start the MongoDB service:
.. code-block:: console
	sudo systemctl start mongod.service

check the service’s status
.. code-block:: console
	sudo systemctl status mongod


Creating recipes
----------------

To retrieve a list of random ingredients,
you can use the ``lumache.get_random_ingredients()`` function:

.. autofunction:: lumache.get_random_ingredients

The ``kind`` parameter should be either ``"meat"``, ``"fish"``,
or ``"veggies"``. Otherwise, :py:func:`lumache.get_random_ingredients`
will raise an exception.

.. autoexception:: lumache.InvalidKindError

For example:

>>> import lumache
>>> lumache.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']

