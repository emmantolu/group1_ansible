# group1_ansible
Group1 Ansible Projects Documentation

This repository documents stages of GROUP1 ansible project execution. 
                    Configuration Management
                                           using Ansible

                                                                                      April 29th 2024




Pre-Configuration

   1. Set up 3 Linux nodes with the following static ip configuration and hostnames
          a. 192.168.100.10 : control
          b. 192.168.100.20 : node1
          c. 192.168.100.30 : node2 (An OracleLinux node)
   2. Map the hostnames to their respective ip addresses on all three machines such that they can all
      ping each other using either hostnames or ip addresses
   3. Ensure that the control machine can ssh into both nodes (a) securely and (b) without using a
      password (Use the ed25519 key type)
   4. Set up a github repository unique to your group. Ensure that
          a. Each member of the group is added to the repository as a contributor
          b. Each member of the group clones the same repo to his/her local machine
NOTE: Going forward, every single question answered MUST be committed and pushed to your
GitHub repo.

Section A

   1. Create an Ansible playbook in your ansible root directory called bootstrap.yml which contains
           a. Code to fully update each node’s software
           b. Code to create an ansible user called “admin”, whose primary group is “admin1” and
              whose secondary groups are “sudo”, “adm” and “root”.
           c. Code to make “admin1” a sudoer
           d. Code to add the ansible ssh-key to each node.
   2. Create an inventory file in your ansible root directory that has both your nodes listed as follows:
           a. Node1 belongs to the “web_servers” group
           b. Node2 belongs to the “db_servers” group
           c. Both Nodes 1 and 2 belong to the “file_servers” group
   3. Create an ansible.cfg file in your ansible root directory. Ensure that it sets the following defaults:
           a. Inventory file
           b. Remote user
           c. Private key file
   4. Create a playbook in your ansible root directory called “server_config.yml” that has does the
      following:
           a. Updates the cache for both “Ubuntu” and “OracleLinux” (or whichever RHEL-based
              distro you have at hand to use for testing).
           b. Installs apache, apache supporting software then starts and enables the software on the
              distro that requires that.



Section B

   1. Group the tasks currently in your server_config.yml and place them under the “web_servers”
      play.
   2. Add a task to the “web_servers” play that :
          a. Updates the current “ServerAdmin” in your apache config file to
              “martin.mato@ingrydacademy.com”
          b. Configures a firewall to ensure that the “http” and “https” ports are open for all web
              servers.
          c. The firewall itself is started and enabled
   3. Create a play called “db_servers” that performs the following tasks
          a. Installs the mySQL database on each node
          b. Starts and enalbes mySQL on the nodes that require this
          c. Assigns the password “mySQLingryd” to the root user on each node
   4. Create a play called “file_servers” that performs the following tasks:
          a. Installs Samba on every file_server node
          b. Starts and Enables Samba on all nodes that require that
          c. Configures the firewall such that the Samba service port is open
            d. Copies a file called “admin_manual” from your ansible root to the /usr/local/bin
               directory of each node. (Create an empty file called admin_manual for this purpose)
            e. Downloads Pycharm Community Edition to each node and saves it in /usr/local/bin



Section C

   1. Add appropriate tags for each task created above
   2. You have a file called “passwords” that you want to transfer to each node. Use “Ansible Vault”
      to transfer the file successfully from your ansible root directory to all nodes. Ensure that this
      runs on ALL hosts.
   3. Create ROLES for each ansible play created above using:
           a. The proper directory structure
           b. The “main.yml” task book for each role
