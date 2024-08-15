General Instructions:

Network Topology

A network topology was implemented in VirtualBox with five VMs: one Controller, one Layer 2 Switch, and three Hosts. VMs introduced realistic network delays, and an overlay network was used to route traffic through the Switch VM, bypassing VirtualBox's internal switching. Each host used Open vSwitch (OVS) with VXLAN tunneling to connect to the Switch VM, which was linked directly to the Controller VM running the Ryu controller.

Traffic Classification

A modified Python script (simple_monitor_13.py) collected network data, which was processed by traffic_classifier.py. This script could:

Collect Training Data for specific traffic types

Classify Traffic using Logistic Regression, Random Forest, Adaboast,Support Vector Machine and Decision Tree (supervised) and K-Means Clustering (unsupervised).

Traffic Simulation

D-ITG simulated traffic flows (Ping, Telnet, DNS, Voice G.711) to train the Machine Learning models. The traffic_classifier.py script collected and transformed flow data, which was stored in CSV files. These files were combined into a Pandas DataFrame for model training and testing.

Jupyter Notebook Implementation

Data Preparation: Load and clean the dataset.
Supervised Learning: Train (Logistic Regression, Random Forest, Adaboast,Support Vector Machine and Decision Tree) models.
Unsupervised Learning: Apply K-Means Clustering to classify traffic.
