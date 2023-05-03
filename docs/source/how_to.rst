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
generates a new perfevent pmda configuration, connects to localhost via ssh, creates a connection with MongoDB and finally registers
the SuperTwin state to database. 

Then, execute_observation_batch_parameters is called from the same superTwin instance. This functions takes three parameters as 
1) path: path in the super computer where the executable commands work.
2) affinity: 
3) commands: a list of commands where each command is in the form of <given name>|<executable command>. The <given name> will be 
the indicator of this command, it will be shown on Grafana generated graphs.

This function executes a batch of observations, where each element in the batch is observed individually and the duration of each 
observation is returned.




