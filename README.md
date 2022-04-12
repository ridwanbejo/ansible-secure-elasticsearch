# How-To Guide for Ansible-Secure-Elasticsearch Playbook

Ansible Secure Elasticsearch installation playbook. It still experimental but I hope I could managed it as Ansible Role.

Follow this guide to run this Ansible playbook.

Prerequisites:

1. Ensure that you have a proper installation of Ansible on your local machine

2. Replace value of these variables in `elasticsearch-install.yml`

```
---
- name: my-elasticsearch
  hosts: elasticsearch
  become: true
  vars:
    es_master_node: "<< your single node >>"
    es_config_path: "/etc/elasticsearch/elasticsearch.yml"
    my_password: "<< your generic password for elasticsearch configuration >>"

...

```

3. Replace value of these variables in `elasticsearch-install.yml`

```
---
- name: my-elasticsearch
  hosts: elasticsearch
  become: true
  vars:
    es_master_node: "<< your master node >>"
    es_unicast_hosts: '["<< your master node >>", "<< your 1st data node >>", "<< your 2nd data node >>"]'
    es_config_path: "/etc/elasticsearch/elasticsearch.yml"
    my_password: "Test@12345"
```

4. Ensure that you have the key pair in your working directory

```
for example:

singapore-region-key-pair
singapore-region-key-pair.pub
```

5. Update Ansible inventory

```
for example:

nano /etc/ansible/hosts

ec2-13-213-77-223.ap-southeast-1.compute.amazonaws.com
ec2-13-213-77-224.ap-southeast-1.compute.amazonaws.com
ec2-13-213-77-225.ap-southeast-1.compute.amazonaws.com
```

6. Run the playbook by using this command if you want to configure single node:

```
ansible-playbook -u ubuntu --private-key singapore-region-key-pair -e 'pub_key=singapore-region-key-pair.pub' elasticsearch-install.yml
```

7. or Run the playbook by using this command if you want to try the cluster mode:

```
ansible-playbook -u ubuntu --private-key singapore-region-key-pair -e 'pub_key=singapore-region-key-pair.pub' elasticsearch-cluster-install.yml
```

# References

- https://aku.dev/create_aws_ec2_instance_with_terraform/
- https://aku.dev/terraform-vpc-introduction/
- https://medium.com/@aliatakan/terraform-create-a-vpc-subnets-and-more-6ef43f0bf4c1
- https://www.digitalocean.com/community/tutorials/how-to-use-ansible-with-terraform-for-configuration-management
- https://blog.gruntwork.io/an-introduction-to-terraform-f17df9c6d180
- https://www.thinkstack.co/blog/using-terraform-to-create-an-ec2-instance-with-cloudwatch-alarm-metrics
