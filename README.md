Playbook-UserParams
-------------------

This is a gcavalcante8808/playbook-userparam repository with an Ansible Playbook.

With this playbook you can deploy git versioned user params to your it infrastructure.

Requirements
------------

To use this playbook you must meet the following requirements:

 * Ansible installed and configured (including access to the targets);
 * Git installed on target hosts;
 * Zabbix Agent installed and configured to read configuration files from /etc/zabbix/zabbix_agentd.conf.d/ directory;
 * Your own userparameter repositories with paramfiles that you want to deploy.

Simple Usage
------------

Clone this repo into your server, access the repo folder created, create your hosts file and use the ansible-playbook to run it:

``` ansible-playbook -i hosts --extra-vars="hosts=<HOSTS> repo_url=<GIT_URL> target_dir=<TARGET_DIR> userparam_file=<FILE> ```

You'll need to provide the following information:

 * hosts: Target Hostgroup;
 * repo_url: Git Clone URL (https or git@, terminated with .git) that have the userparameter and its scripts (if exists); will be cloned to target machines;
 * target_dir: Host directory where the repo_url will be cloned. Eg: /usr/local/src/zbx-mysql for an github.com/gcavalcante8808/zbx-mysql.git;
 * userparam_file: UserParam file name that will be copied to /etc/zabbix/zabbix_agentd.conf.d/ directory.

Example
-------

The following example will use the userparam file available at github.com/gcavalcante8808/zbx-mysql.git to deploy mysql params to all hosts. The steps are the following:

1. Clone this repository into a folder in a server that have ansible installed:

``` cd /tmp && git clone https://github.com/gcavalcante8808/playbook-params.git && cd /tmp/playbook-params/ ```

2. Run the playbook with all needed configuration to deploy mysql params:

``` ansible-playbook -i hosts playbook.yml -e "hosts=all repo_url=https://github.com/gcavalcante8808/zbx-mysql.git target_dir=/usr/local/src/zbx-mysql userparam_file=mysql.conf```

3. Profit!

Other Info
----------

Another notes about this playbook:

 * The playbook was tested with ansible core(cli) and Semaphore;
 * Pay Attention to the target dir for userparams that relies on scripts to extract data (the path problem can be tricky to debug on zabbix-agent);
 * ** THE PLAYBOOK REMOVES A FILE WITH SAME NAME OF <userparam_file> IF IT IS PRESENT ON THE /etc/zabbix/zabbix_agentd.conf.d/ AND PUT A SYMLINK IN PLACE. **;
Author
------

Author: Gabriel Abdalla Cavalcante Silva (gabriel.cavalcante88@gmail.com)
