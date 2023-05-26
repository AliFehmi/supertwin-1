How To Guides
=============

.. _how_to:

.. autosummary::
   :toctree: generated

   lumache

This section includes guides on how to perform certain actions using the SuperTwin.

1) How to create SuperTwin instance?
++++++++++++++++++++++++++++++++++++
To create a SuperTwin instance, you need to run supertwin.py file after you start
mongodb, grafana-server and influxdb. In this file, SuperTwin class constructor is called. Inside
this constructor, __build_twin_from_scratch method is called. Since no arguments are
given in the command previously run, this function asks 4 inputs for the user to enter, the address
of the remote system, and the hostname.

The function named main is called which is defined in remote_probe.py that performs
remote probing in Linux. Firstly, this function prompts the user to enter the SSH username and
password. The paramiko library is used to create an SSH client object. It creates an instance of
the SSHClient class from the paramiko library and assigns it to the ssh variable. This object
represents an SSH client session that can be used to connect to a remote system and execute
commands over an encrypted channel.

Later, it sets the policy for automatically adding the remote system's host key to the local
system's known_hosts file. This is done to prevent potential security risks, such as a
man-in-the-middle attack.

The function then connects to the remote host using SSH and executes the "hostname"
command to obtain the name of the remote host. The function then creates two directories on the
remote system and copies files from the local system to the remote system using Secure Copy
(SCP).

The scp.put() method is used to copy a file or directory from the local system to a
remote system over an encrypted SCP (Secure Copy) connection.

The pmu_query_path variable holds the path of the file or directory to be copied, and the
recursive parameter is set to True to recursively copy the entire directory and its contents.
The remote_path parameter specifies the destination path on the remote system where the
file or directory will be copied to.

After copying the files, the function runs several commands on the remote system,
including removing files, creating files, compiling code, and running Python scripts. Finally, the
function retrieves the probing results from the remote system using SCP and saves them to a file.
The scp.get() method is used to download a file or directory from the remote system
to the local system over an encrypted SCP (Secure Copy) connection.
The function returns the remote host name, the probing results file name, SSH username,
and SSH password.

The function read_env() reads environment variables from a file named "env.txt" and
returns a tuple containing the values of four specific variables: "MONGODB_SERVER",
"INFLUX_1.8_SERVER", "GRAFANA_SERVER", and "GRAFANA_TOKEN". This txt file
contains the ports that run the Influx, Grafana and MongoDB servers and the tokens.

The function create_grafana_datasource() is used to create a datasource in
Grafana for connecting to an InfluxDB server. It takes several parameters:
● hostname: The hostname used to identify the datasource.
● uid: A unique identifier used to identify the datasource.
● api_key: The API key used for authentication with Grafana.
● grafana_server: The URL of the Grafana server.

2) How to generate dashboards on Grafana?
+++++++++++++++++++++++++++++++++++++++++

In the SuperTwin repository, you will find pmu_demo.py file which shows an example of how to generate a dashboard.


In this file, a superTwin instance is created by giving the IP address of the computer that you want the test to be conducted on 
as a parameter.

Later, ``reconfigure_observation_events_parameterized`` function is called from the supertTwin object by giving the txt file which 
includes the performance observation metric names to test.This function reads the txt file, saves the observation metrics. It 
generates a new perfevent pmda configuration, connects to remote host via ssh, creates a connection with MongoDB and finally registers
the SuperTwin state to database. 

Then, ``execute_observation_batch_parameters`` is called from the same superTwin instance. This functions takes three parameters as 

**1) path:** path in the super computer where the executable commands work.

**2) affinity:** likwid-pin which is a command line application to pin a sequential or multithreaded applications to dedicated 
processors is used here along with necessary options.

**3) commands:** a list of commands where each command is in the form of <given name>|<executable command>. The <given name> will be 
the indicator of this command, it will be shown on Grafana generated graphs.

This function executes a batch of observations, where each element in the batch is observed individually. It configures InfluxDB
server and PCP, connects to remote host via ssh and runs the commands on remore host, saves the outputs on InfluxDB,
creates dashboard on Grafana, queries the observation results from DB and uploads it to Grafana.

In the end of this run, a url to access the Grafana dashboard will be printed on the screen. Graphs and mean charts for each observation
are generated on this dashboard.




