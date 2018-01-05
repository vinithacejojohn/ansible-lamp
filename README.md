# ansible-lamp

This playbook provisions a LAMP server in EC2 instances. Its a single playbook with default variables inside `default/main.yml` so you may change the values as required. This repo uses an Ubuntu AMI by default, so we need to explicitly mention `python3` for ansible to run, which is given in `group_vars/all.yml`.

The playbook has two plays, the first one provisions the instances and the second one will install and configure packages. The second play has two host groups `webservers` and `tag_Name_lamp`. Both host groups have the same targets but the former makes ansible to select the hosts from the in-memory inventory created by the first play when instances are launched. The second group is used when the playbook is run at a later time when the instances are already provisioned and it uses the tag assigned to the instances.

### Requirements

* AWS credentials should be set in any of the standard ways
* `boto` library should be installed and have `ec2.py` as inventory
* EC2 key-pair private key

### Run the playbook

If you have ec2.py downloaded in the repo, run the below command. Replace `PATH-TO/SSH-KEY` with the path to the private key of your EC2 key-pair.

```
ansible-playbook -i ec2.py -e "ssh_key_path=PATH-TO/SSH-KEY" lamp.yml
```
