# ansible-consul

#Usage

consul-server-setup.yml

- hosts: #your host file name or dynamic tag/group value in case of dynamic inventory
  become: yes

  vars:
    consul_server: yes
    consul_mode: "server"
    consul_dir:  #location of your consul installation
    consul_data_dir:  "{{ consul_dir }}/data"
    consul_conf_dir:  "{{ consul_dir }}/conf"
    consul_conf_datacenter: #datacenter name of your choice
    consul_conf_bootstrap_expect:  #number of instance of consul you want to run in server mode.
    consul_domain:  #custom dns name of using consul dns
    consul_conf_bind_addr: 0.0.0.0
    consul_conf_client_addr: 0.0.0.0
    consul_agent: no
    consul_recursor: #upstream DNS server (the one in resolv.conf for any dns resolution outside consul domain)

  roles:
    - role: ansible-consul

consul-agent-setup.yml 

- hosts:  #your host file name or dynamic tag/group value in case of dynamic inventory
  become: yes

  vars:
    consul_mode: "agent"
    consul_dir: #location of your consul installation
    consul_data_dir:  "{{ consul_dir }}/data"
    consul_conf_dir:  "{{ consul_dir }}/conf"
    consul_conf_datacenter: #datacenter name of your choice
    consul_conf_bootstrap_expect: #number of instance of consul you want to run in server mode.
    consul_domain: #custom dns name of using consul dns
    consul_conf_bind_addr: 0.0.0.0
    consul_conf_client_addr: 0.0.0.0
    consul_agent: yes
    consul_server: no

  roles:
    - role: ansible-consul

#FOR STATIC INVENTORY
---------------------

ansible-playbook -i hosts consul-server-setup.yml # To setup consul in server mode

ansible-playbook -i hosts consul-agent-setup.yml  # To setup consul in agent mode


#FOR DYNAMIC INVENTORY IN CASE OF AWS
-------------------------------------

ansible-playbook -i ec2.py consul-server-setup.yml # To setup consul in server mode

ansible-playbook -i ec2.py consul-agent-setup.yml  # To setup consul in agent mode

Please note in case of dynamic inventory please edit the agent.json and server.json host group values to the tag_ in ec2.py host group.
