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
this constructor, ``__build_twin_from_scratch`` method is called. Since no arguments are
given in the command previously run, this function asks 4 inputs for the user to enter, the address
of the remote system, and the hostname.

The function named ``main`` is called which is defined in remote_probe.py that performs
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

The ``scp.put()`` method is used to copy a file or directory from the local system to a
remote system over an encrypted SCP (Secure Copy) connection.

The ``pmu_query_path`` variable holds the path of the file or directory to be copied, and the
recursive parameter is set to True to recursively copy the entire directory and its contents.
The remote_path parameter specifies the destination path on the remote system where the
file or directory will be copied to.

After copying the files, the function runs several commands on the remote system,
including removing files, creating files, compiling code, and running Python scripts. Finally, the
function retrieves the probing results from the remote system using SCP and saves them to a file.
The ``scp.get()`` method is used to download a file or directory from the remote system
to the local system over an encrypted SCP (Secure Copy) connection.
The function returns the remote host name, the probing results file name, SSH username,
and SSH password.

The function ``read_env()`` reads environment variables from a file named "env.txt" and
returns a tuple containing the values of four specific variables: "MONGODB_SERVER",
"INFLUX_1.8_SERVER", "GRAFANA_SERVER", and "GRAFANA_TOKEN". This txt file
contains the ports that run the Influx, Grafana and MongoDB servers and the tokens.

The function ``create_grafana_datasource()`` is used to create a datasource in
Grafana for connecting to an InfluxDB server. It takes several parameters:

● hostname: The hostname used to identify the datasource.

● uid: A unique identifier used to identify the datasource.

● api_key: The API key used for authentication with Grafana.

● grafana_server: The URL of the Grafana server.

The function begins by setting the necessary headers for the API request. It includes the
Authorization header with the provided api_key and sets the Content-Type header to
"application/json".

Next, a dictionary data is created to define the properties of the datasource. It includes the
name of the datasource, which combines the hostname and uid, and sets the type to "influxdb".
The url property is set to the influxdb_server URL, and the database property is set to the
hostname. The access property is set to "proxy" to allow Grafana to proxy requests to the
InfluxDB server, and basicAuth is set to False to indicate that basic authentication is not used.

The function then makes a POST request to the Grafana API endpoint for creating
datasources (/api/datasources). It sends the data dictionary as JSON in the request body and
includes the headers for authentication. The verify parameter is used to control SSL/TLS
certificate verification. It returns the response JSON content as a dictionary.

The function get_pcp_pids() begins by creating an SSH client object using
paramiko.SSHClient() and sets the missing host key policy to automatically add the remote
system's host key. It then establishes an SSH connection to the remote system using the provided
address, SSH username, and password.

The function executes the command ps aux | grep pcp on the remote system using
ssh.exec_command(). This command lists all running processes (ps aux) and filters the output to
only show lines containing the string "pcp" (grep pcp). The function reads the output from the
command and stores it in the output variable.

The function initializes an empty dictionary pids to store the process IDs of the PCP
processes.

It then iterates over each line in the output and checks for specific PCP process names
using item.find().

Finally, the function prints the modified pids dictionary and returns it as the result of the
function.

get_influx_database parses an address string to extract the host and port
information, and then returns an InfluxDBClient object initialized with the extracted host and
port values for connecting to an InfluxDB server.

create_influx_database function creates a new database with the specified name
using the provided InfluxDB data source

create_database creates a new database in InfluxDB

insert_twin_description function inserts a twin description document into a
MongoDB collection. It retrieves relevant information from the provided supertwin object, such
as hostname, address, date, and various configuration details. The document is inserted into the
"twin" collection, and the ID of the inserted document is returned

get_mongo_database establishes a connection to a MongoDB server using the
provided connection string. It then returns the specified MongoDB database with the given
name.

get_twin_description_from_file reads a JSON file specified by hostProbFile,
loads its content into a dictionary _sys_dict, and passes that dictionary along with other
parameters (alias, SSHuser, SSHpass, addr) to a function generate_dt.main() to generate a twin
description _twin. The generated twin description is then returned.

pmu_to_pcp converts PMU (Performance Monitoring Unit) metrics into PCP
(Performance Co-Pilot) metric names and appends them to the metrics list. It iterates over each
key in the PMUs dictionary. If the key does not contain the substring "perf", it checks if the key
should be added based on whether it has already been added to the added list. If it should be
added, it iterates over the events associated with that key and appends the corresponding PCP
metric name, original metric name, and event value to the metrics list. The added list keeps track
of the keys that have been processed to avoid duplicates.

add_my_metrics_mapped adds metrics to a dictionary of models. It retrieves specific
metrics based on given categories, maps them to the appropriate format, and appends them to the
dictionary under the corresponding model.

add_cpus It iterates over each key in the PMUs dictionary. If the key does not contain
the substring "perf", it checks if the key should be added based on whether it has already been
added to the added list. If it should be added, it iterates over the events associated with that key
and appends the corresponding PCP metric name, original metric name, and event value to the
metrics list. The added list keeps track of the keys that have been processed to avoid duplicates.
Finally, the function returns the updated metrics list.

add_memory function adds custom metrics to a dictionary based on provided
parameters, appending either a supertwin telemetry or regular telemetry based on the type of the
custom metric. The updated dictionary is returned.

add_disk function adds a disk component to a digital twin represented by a dictionary
(models_dict) based on the provided parameters. It connects the disk component to the system,
adds properties and custom metrics as telemetry, and calls another function add_phy_disks() to

add physical disks. The updated models_dict is returned.

add_network function adds a network component to a digital twin represented by a
dictionary (models_dict) based on the provided parameters. It connects the network component
to the system, adds custom metrics as telemetry, and calls another function add_subnets() to add
subnets. The updated models_dict is returned.

get_pcp_pids_by_credentials adds a network component to a digital twin
represented by a dictionary (models_dict) based on the provided parameters. It creates a top-level
network interface, connects it to the system, adds custom metrics as telemetry, and calls another
function add_subnets() to add subnets. The updated models_dict is returned.

get_monitoring_metrics retrieves monitoring metrics from a supertwin object
based on the specified metric type. It accesses a database, extracts the twin data, and filters out
metrics that match the given metric type. The function then returns a list of dictionaries, where
each dictionary contains the metric name and its corresponding type.

get_metric_type function determines the type of a metric based on the given metric
name. It checks for specific patterns in the metric name and assigns the corresponding type. The
function returns a string representing the type of the metric.
reconfigure_observation_events_beginning used to reconfigure the
observation events at the beginning. It first checks for metrics that should always be present in
the "observation_metrics" list and adds them if they are missing. Then, it calls the

"reconfigure_perfevent()" method and registers the twin state using the "register_twin_state()"
function from the "utils" module. There is commented out code that writes the metrics to a file
named "last_observation_metrics.txt".

reconfigure_perfevent is used to reconfigure the "perfevent" component on a
remote server. It establishes an SSH connection to the server using the provided credentials.
Then, it uses SCP to transfer a file named "perfevent.conf" to a temporary location on the server.
It creates a shell script named "reconfigure_perf.sh" that contains a series of commands to
perform the reconfiguration. The shell script is also transferred to the server. Finally, it executes
the shell script with sudo privileges on the remote server to reconfigure the "perfevent"
component. A message is printed to indicate that the remote "perfevent" pmda has been
reconfigured.

generate_perfevent_conf function is used to generate a new configuration file for
the "perfevent" pmda component. It takes a "SuperTwin" object as input. It retrieves the
observation metrics from the object and ensures that any metrics that should always be present
are included. It also retrieves the MSR (Model-Specific Register) configuration using the
"get_msr()" function from the "utils" module.

reconfigure_perfevent The function then creates a new file named
"perfevent.conf" and writes the MSR configuration and the list of metrics to it. Finally, it prints a
message to indicate that a new configuration for the "perfevent" pmda has been generated. The
function then creates a new file named "perfevent.conf" and writes the MSR configuration and
the list of metrics to it. Finally, it prints a message to indicate that a new configuration for the
"perfevent" pmda has been generated.

generate_pcp2influx_config generates a configuration file for PCP2InfluxDB
integration based on the attributes of a "SuperTwin" object. It retrieves the necessary information
such as database name, tags, source IP, and metrics. It then constructs the configuration file by
adding options, including InfluxDB server details and source information, as well as the
specified metrics. The resulting configuration file is written to disk, and the file name is returned.

update_state updates the state by appending a new line of information to a file
named "supertwin.state". It takes in the parameters name, addr, twin_id, and collection_id, and
writes them in a specific format separated by the "|" character. The function then closes the file
after writing the information.

kill_zombie_monitors This function is used to kill zombie monitoring samplers
running on the system. It retrieves the process information for processes matching the name
"/usr/bin/pcp2influxdb" by executing the command "ps aux | grep pcp2influxdb". It extracts the
process ID, state, and configuration file from the output and compares the process ID with the
monitor_pid attribute. If they do not match, it forcefully kills the process.

generate_monitoring_dashboard generates a monitoring dashboard using the
generate_monitoring_dashboard() function from the monitoring_dashboard module. It assigns
the generated URL of the dashboard to the variable url. Then, it calls the
update_twin_document__add_monitoring_dashboard() method of the current object, passing the
URL as a parameter to update the twin document with the monitoring dashboard URL.
generate_monitoring_dashboard is responsible for generating a monitoring
dashboard. It calls the generate_monitoring_dashboard() function from the
monitoring_dashboard module, passing self as an argument. The generated dashboard URL is
assigned to the variable url. Then, it calls the update_twin_document__add_monitoring_dashboard()
method of the current object, passing the URL as a parameter to update the twin document by
adding the monitoring dashboard URL.

get_params_interface_known retrieves the parameters for a known interface and
measurement from a twin description (td). It iterates over the contents of the specified interface
in the twin description and checks if the content's type contains "Telemetry". If a content's
database name matches the provided measurement, it assigns the content's display name as the
"Param" parameter and the interface's display name as the "Alias" parameter in the params
dictionary. There is a special case for the measurement "hinv_cpu_clock" where the first
content's display name is used instead. If the "Alias" contains the word "thread", it is stripped for
a cleaner appearance. The function then returns the params dictionary.

update_twin_document__add_monitoring_dashboard updates the twin
document by adding a monitoring dashboard URL. It retrieves the MongoDB database for the
twin using the twin's name and MongoDB address. Then, it retrieves the twin document
associated with the current object's MongoDB ID. The retrieved document is modified by adding
a new key-value pair with the key "monitoring_dashboard" and the provided URL as the value.
Finally, the modified document is replaced in the database using the twin's MongoDB ID. A
message is printed to indicate that the monitoring dashboard has been added to the digital twin.
register_twin_state registers the state of a twin by updating its twin
document in the MongoDB database. It retrieves the twin document based on the twin's name
and MongoDB address. Then, it updates the relevant fields in the document with the
corresponding values from the SuperTwin object. The modified document is replaced in the
database, and a message is printed to indicate that the twin state has been registered.

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




