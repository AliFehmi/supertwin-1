How To Guides
=============

.. _how_to:

.. autosummary::
   :toctree: generated

   lumache

This section includes guides on how to perform certain actions using the SuperTwin.

How to generate dashboards on Grafana?
--------------------------------------

In the SuperTwin repository, you will find pmu_demo.py file which shows an example of how to generate a dashboard.


In this file, a superTwin instance is created by giving the IP address of the computer that you want the test to be conducted on 
as a parameter.

Later, reconfigure_observation_events_parameterized function is called from the supertTwin object by giving the txt file which 
includes the performance observation metric names to test.This function reads the txt file, saves the observation metrics. It 
generates a new perfevent pmda configuration, connects to remote host via ssh, creates a connection with MongoDB and finally registers
the SuperTwin state to database. 

Then, execute_observation_batch_parameters is called from the same superTwin instance. This functions takes three parameters as 

1) path: path in the super computer where the executable commands work.

2) affinity: likwid-pin which is a command line application to pin a sequential or multithreaded applications to dedicated 
processors is used here along with necessary options.

3) commands: a list of commands where each command is in the form of <given name>|<executable command>. The <given name> will be 
the indicator of this command, it will be shown on Grafana generated graphs.

This function executes a batch of observations, where each element in the batch is observed individually. It configures InfluxDB
server and PCP, connects to remote host via ssh and runs the commands on remore host, saves the outputs on InfluxDB,
creates dashboard on Grafana, queries the observation results from DB and uploads it to Grafana.

In the end of this run, a url to access the Grafana dashboard will be printed on the screen. Graphs and mean charts for each observation
are generated on this dashboard.




