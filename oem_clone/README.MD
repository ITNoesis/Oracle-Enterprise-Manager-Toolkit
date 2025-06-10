Access the dedicated repository for OEM Clone at 

https://github.com/ITNoesis/OEM_Clone.git

# OEM_Clone - Beta
Automate the Oracle Enterprise Manager (OEM) Cloud Control OMS Cloning process using Ansible. Supported OEM versions: 13.4 and 13.5

# This code is still in its beta stage and being tested. I DO NOT recommend to use this in production as of now.
If you get an opportunity to test. Let me know how it went

# Suggestions and contributions are most welcome!

# OEM OMS Clone Automation using Ansible

This repository provides a fully automated Ansible playbook to clone Oracle Enterprise Manager (OEM) Cloud Control OMS to a new Linux server. With the exception of cloning the repository database and assumes that the database clone has been performed successfully. I plan to add a role for db_duplicate in a future release. 

---

## Supported OEM Versions:
- Oracle Enterprise Manager 13.4
- Oracle Enterprise Manager 13.5

---

## High-Level Steps Performed:
- Copy EMKey to repository
- Clone OEM repository database (manual step, validation included)
- Create and copy OMS binary
- Install Agent in `softwareOnly` mode
- Automatically detect OEM version
- Conditional execution of OPSS schema recreation for OEM 13.4 and below
- OMS clone
- Plugin configuration
- OMS startup and validation
- Agent configuration and health check

---

## Prerequisites:

- Python 3 and Ansible 2.10+
- Oracle user access on source and target servers
- Manual clone of the repository DB via RMAN (this is validated, not performed)
- All binaries: agent ZIP, OMS clone JAR, software library tar file should be prepared and copied beforehand

---

## Variables:

Update the following:
```yaml
oracle_home: /u01/app/oracle/product/em135
oms_clone_jar: /refresh/clone/oms_clone.jar
agent_base: /refresh1/agent135
agent_software: /tmp/13.5.0.0.0_AgentCore_226.zip
em_domain_name: EM135_CLONE
repo_conn_str: "(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=dbhost)(PORT=1521))(CONNECT_DATA=(SID=EMREP)))"
plugin_list: "oracle.sysman.db,oracle.sysman.emas,oracle.sysman.oh"
msport: 7102
cloned_oms_hostname: newoms.example.com
agent_port: 3872
upload_port: 4889
agent_reg_password: mysecretpassword
sys_password: my_sys_password
sysman_password: my_sysman_password
```
---
# Running the Playbook
```shell
ansible-playbook -i your_inventory_loc/hosts.yml clone_oms.yml -f 1 -e 'source_server=<Source_OEM_Server> target_server=<Target_OEM_Server>'
```
---
# Notes

OPSS schema recreation is automatically triggered if OEM version ≤ 13.4.
Ensure database connectivity, permissions, and binaries are in place before starting.
DB cloning via RMAN must be handled manually but validated by this playbook.

---
# Contributing
Pull requests and issues are welcome. Please ensure any changes are tested in both 13.4 and 13.5 environments.

Thanks and I hope it helps!
