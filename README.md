Network Topology Implementation
A network topology was implemented using VirtualBox, consisting of five Virtual Machines (VMs): one Controller, one Layer 2 Switch, and three Hosts. The network was designed with VMs to introduce realistic network delays. Instead of using Mininet, which simulates the network within a single VM, an overlay network was deployed to ensure that traffic between hosts would pass through the Switch VM rather than using VirtualBox's internal switching mechanism.

Each host was configured with Open vSwitch (OVS) and two network interfaces. The first interface was internal, while the second connected to the Switch VM using VXLAN tunneling. The Switch VM, also running OVS, had VXLAN interfaces connected to the hosts and a direct connection to the Controller VM using an underlay IP. The Ryu controller was deployed on the Controller VM to manage network traffic. Once the network was successfully deployed and configured, the controller could monitor the packets flowing through the switch between any of the hosts.

Traffic Classification
A Python script, simple_monitor_13.py, was modified and used to collect network data. This data was then fed into the traffic_classifier.py script, which performed the following tasks:

Collect Training Data: The script collected training data for specified traffic types. The traffic had to be flowing between two hosts before the script was executed.
Supervised Machine Learning: The script used Logistic Regression to classify the type of traffic flow between hosts.
Unsupervised Machine Learning: The script employed K-Means Clustering to classify the traffic type in an unsupervised manner.
Traffic Simulation with D-ITG
The Distributed Internet Traffic Generator (D-ITG) was used to simulate traffic flows for training the Machine Learning models. D-ITG is capable of generating IPv4 and IPv6 traffic by accurately replicating the workload of various Internet applications, following stochastic models for packet size (PS) and inter-departure time (IDT) to mimic application-level protocol behavior. For this proof of concept, the following traffic types were simulated: Ping, Telnet, DNS, and Voice (G.711 codec).

The process for collecting training data involved simulating the flow of specific traffic types between pairs of hosts using D-ITG or other tools. The traffic_classifier.py script was then started with the appropriate options for the traffic type, which also initiated the Ryu controller and the modified monitoring script (simple_monitor_AK.py). The generated data was collected, transformed to update the attributes of a Flow object, and periodically outputted to a CSV file. Once CSV files were generated for each traffic type, they were combined into a complete Pandas DataFrame used for model training and testing.

In Jupyter Notebook follows the following steps:
1. Loading and Cleaning Data
2. Supervised Model - Logistic Regression
3. Unsupervised Model - K-Means Clustering
