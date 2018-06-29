# ansible-consul

#Usage

#For Static Inventory
---------------------

ansible-playbook -i hosts consul-server-setup.yml # To setup consul in server mode

ansible-playbook -i hosts consul-agent-setup.yml  # To setup consul in agent mode


#For Dynamic inventory in case of AWS
-------------------------------------

ansible-playbook -i ec2.py consul-server-setup.yml # To setup consul in server mode

ansible-playbook -i ec2.py consul-agent-setup.yml  # To setup consul in agent mode

Please note in case of dynamic inventory please edit the agent.json and server.json host group values to the tag_ in ec2.py host group.
