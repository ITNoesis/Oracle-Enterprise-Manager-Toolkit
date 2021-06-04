ansible-role-oracle-oem-agent-deploy
=========

This role is to deploy Oracle Enterprise Manager agents on target hosts running Linux operating system. The role has been tested on multiple servers running Oracle Enterprise Linux 6 and 7.

Requirements
------------

The role requires the agent media to be downloaded and placed in a folder on the ansible-controller. In absence of the install media, the role will simply fail asking for the file.

Role Variables
--------------

The variables are stored in defaults/main.yml.

    oem_user: oraoem
    oem_user_group: oinstall
    oem_user_id: 15011
    agent_port: 3900
    agent_upload_port: 4903
    oms_host: server.company.com
    oemagent_base: /Monitoring/OEM13_4
    oem_reg_passwd: Strong_Password@123##
    # Place the OEM agent media on ansible controller
    oem_agent_media: 13.4.0.0.0_AgentCore_226.zip
    oem_agent_media_dir: /tmp/Agent_Media
    oem_temp_dir: /tmp/ansible_emagent
    oem_agent_version: 13.4.0.0.0
    central_server: ansiblecontroller.company.com hosts: servers

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
        role: oracle-oem-agent-deploy

License
-------

BSD

Author Information
------------------

Arun Yadav (ITNoesis) and Vibek Kumar (VIBEKKUM)
