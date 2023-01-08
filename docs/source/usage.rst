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

   It is important that you install the correct versions.

.. note::

   In the SuperTwin repository, you can find a directory called setup which automizes the setup process by detecting your operating system. 
   You can run it to install required dependencies and libraries all at once.
   

1) Ubuntu 20.04
+++++++++++++++


1.1) MongoDB Installation

Import the public GPG key

.. code-block:: console

   wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -

The operation should respond with an OK.

.. note::

   If you receive an error indicating that gnupg is not installed:

   .. code-block:: console

      sudo apt-get install gnupg

   Then retry the first command.

   
Create a file in the sources.list.d directory named mongodb-org-4.4.list

.. code-block:: console

   echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list

Reload the local package database:

.. code-block:: console

   sudo apt-get update

Install MongoDB

.. code-block:: console

   sudo apt-get install -y mongodb-org

Start the MongoDB service:

.. code-block:: console

   sudo systemctl start mongod

.. note:: 

   If you receive an error similar to this: Failed to start mongod.service: Unit mongod.service not found.

   .. code-block:: console 

      sudo systemctl daemon-reload

   Then, run the above command again.

Check the service’s status

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

Add the InfluxData repository

.. code-block:: console

   wget -q https://repos.influxdata.com/influxdb.key
   
Setup the repository

.. code-block:: console

   echo '23a1c8836f0afc5ed24e0486339d7cc8f6790b83886c4c96995b88a061c5bb5d influxdb.key' | sha256sum -c && cat influxdb.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/influxdb.gpg > /dev/null
   echo 'deb [signed-by=/etc/apt/trusted.gpg.d/influxdb.gpg] https://repos.influxdata.com/debian stable main' | sudo tee /etc/apt/sources.list.d/influxdata.list
   
Update your server and install InfluxDB 1.8

.. code-block:: console

   sudo apt-get update && sudo apt-get install influxdb

Unmask the service (Required for Ubuntu 15.04+)

.. code-block:: console

   sudo systemctl unmask influxdb.service

Start InfluxDB Service 

.. code-block:: console

   sudo systemctl start influxdb

Check the status to see if it runs correctly

.. code-block:: console

   sudo systemctl start influxdb

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

1.5) Install pcp-export-pcp2influxdb
You can download it from https://packages.debian.org/sid/utils/pcp-export-pcp2influxdb based on the architecture of your computer.

1.6) Install additional requirements

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

1.7) Run the server

Clone the repository

.. code-block:: console
   
   git clone https://github.com/sparcityeu/Digital-SuperTwin.git

If you have Dolap account, you can activate it:

.. code-block:: console
   
   ssh <your username>@10.36.54.195

Inside of the SuperTwin directory:

.. code-block:: console
   
   sudo python3 supertwin.py

When it is asked, enter the address as 10.36.54.195 and your credentials.

.. warning::

   Before you run the server, make sure that you start MongoDB, InfluxDB and Grafana.



2) Manjaro
++++++++++

3) Mac
++++++
3.1) XCode Developer Tools

Install XCode developer tools using the command below

.. code-block:: console

   xcode-select --install


3.2) Homebrew

Install homebrew by using the following command

.. code-block:: console

   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"


3.3) MongoDB

tap mongodb homebrew tap

.. code-block:: console

   brew tap mongodb/brew

updating homebrew

.. code-block:: console
   
   brew update

installing mongodb

.. code-block:: console
   
   brew install mongodb-community@6.0



3.4) InfluxDB

Install influxdb using homebrew

.. code-block:: console

   brew install influxdb


3.5) Grafana

Install Grafana using homebrew

.. code-block:: console

   brew install grafana


3.6) MongoDB Compass 

Install MongoDB Compass using the link: https://www.mongodb.com/docs/compass/current/install/




   