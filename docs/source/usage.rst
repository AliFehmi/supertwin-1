Usage
=====

.. _installation:

Installation
------------

You can find the necessary technologies, packages, libraries and how to install them based on your operating system below:

On local host

You need

- InfluxDB 1.8
- MongoDB
- Grafana 9+
- Plugins
- JSON
- Node Graph API
- Plotly panel
- pcp-export-pcp2influxdb
- Python 3.7+

.. warning::

   It is important that you need to install the correct versions.

1) Ubuntu 20.04
---------------

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

.. code-block:: console

   sudo -i

Download the GPG key

.. code-block:: console

   wget -qO- https://repos.influxdata.com/influxdb.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/influxdb.gpg > /dev/null

Setup the repository

.. code-block:: console

   export DISTRIB_ID=$(lsb_release -si); export DISTRIB_CODENAME=$(lsb_release -sc)
echo "deb [signed-by=/etc/apt/trusted.gpg.d/influxdb.gpg] https://repos.influxdata.com/${DISTRIB_ID,,} ${DISTRIB_CODENAME} stable" | sudo tee /etc/apt/sources.list.d/influxdb.list > /dev/null

Update your server

.. code-block:: console

   apt-get update

Install InfluxDB2

.. code-block:: console

   apt-get install influxdb2

Start InfluxDB Service 

.. code-block:: console
   systemctl start influxdb
   systemctl status influxdb

1.4) Grafana Installation

Install the dependencies

.. code-block:: console

   apt-get install wget curl gnupg2 apt-transport-https software-properties-common -y

Add the Grafana GPG key

.. code-block:: console
   wget -q -O - https://packages.grafana.com/gpg.key | apt-key add -

Add the Grafana repository

.. code-block:: console
   echo "deb https://packages.grafana.com/oss/deb stable main" | tee -a /etc/apt/sources.list.d/grafana.list

Update your server

.. code-block:: console

   apt-get update

Install Grafana

.. code-block:: console

   apt-get install grafana -y

Start Grafana service:

.. code-block:: console

   systemctl start grafana-server
   systemctl status grafana-server

Connect to localhost:3000/ and enter your credentials. Under the configurations drop-down, select plugins and install the following plugins:
JSON
Node Graph API
Plotly Panel

1.5) Install additional requirements

.. code-block:: console

   pip install cryptography==2.8
   pip install Flask==2.2.2
   pip install Flask_Cors==3.0.10
   pip install grafanalib==0.6.3
   pip install influxdb==5.3.1
   pip install matplotlib==3.4.1
   pip install numpy==1.17.4
   pip install pandas==1.5.1
   pip install paramiko==2.6.0
   pip install plotly==5.11.0
   pip install pymongo==4.1.1
   pip install requests==2.22.0
   pip install scp==0.14.4

1.6) Run the server

Clone the repository

.. code-block:: console
   
   git clone https://github.com/sparcityeu/Digital-SuperTwin.git

If you have Dolap account,you can activate it:

.. code-block:: console
   
   ssh <your username>@10.36.54.195

Inside of the SuperTwin directory:

.. code-block:: console
   
   sudo python3 supertwin.py

When it is asked, enter the address as 10.36.54.195 and your credentials.


2) Manjaro
----------

3) Mac
------
