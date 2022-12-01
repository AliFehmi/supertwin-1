Usage
=====

.. _installation:

Installation
------------

You can find the necessary technologies, packages, libraries and how to install them based on your operating system below:

1) UBUNTU 20.04 lolok

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
   
1.2) MongoDB Compass Installation

Download the MongoDB compass .deb file 

.. code-block:: console
   wget https://downloads.mongodb.com/compass/mongodb-compass_1.28.1_amd64.deb
Install the .deb file
.. code-block:: console
   sudo apt install ./mongodb-compass_1.28.1_amd64.deb
Open the application and click on the connect button.

1.3) InfluxDB Installation

Switch to the root user
sudo -i

Download the GPG key
wget -qO- https://repos.influxdata.com/influxdb.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/influxdb.gpg > /dev/null

Setup the repository
export DISTRIB_ID=$(lsb_release -si); export DISTRIB_CODENAME=$(lsb_release -sc)
echo "deb [signed-by=/etc/apt/trusted.gpg.d/influxdb.gpg] https://repos.influxdata.com/${DISTRIB_ID,,} ${DISTRIB_CODENAME} stable" | sudo tee /etc/apt/sources.list.d/influxdb.list > /dev/null
Update your server
apt-get update
Install InfluxDB2
apt-get install influxdb2
Start InfluxDB Service 
systemctl start influxdb
systemctl status influxdb

1.4) Grafana Installation
Install the dependencies
apt-get install wget curl gnupg2 apt-transport-https software-properties-common -y
Add the Grafana GPG key
wget -q -O - https://packages.grafana.com/gpg.key | apt-key add -
Add the Grafana repository
echo "deb https://packages.grafana.com/oss/deb stable main" | tee -a /etc/apt/sources.list.d/grafana.list
Update your server
apt-get update
Install Grafana
apt-get install grafana -y
Start Grafana service:
systemctl start grafana-server
systemctl status grafana-server

Connect to localhost:3000/ and enter your credentials. Under the configurations drop-down, select plugins and install the following plugins:
JSON
Node Graph API
Plotly Panel


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

