# cat9k-ipsec-ansible-private

This playbook covers site-2-site site-2-multisite scenarios.

In group_vars:
all.yml - Here are credentials to connect to C9Ks (info is used here for both scenarios)
hub.yml - Here are credentials that the hub needs to connect to both Spoke 1 and Spoke 2 (this is only used for the site-2-multisite scenario)
In host_vars:
There is info the covers the site-2-site scenario.
site-1.yml - info to connect to site-2
site-2.yml - into to connect to site-1

Running scenarios:
    site-2-site:
Changes need to be done in host_vars file in order to have connectivity. Make sure that in /group_vars/all.yml are the correct credentials for SSHing into C9Ks.
Create tunnel
ansible-playbook -i ./hosts ./site-to-site-up.yml
Delete tunnel
ansible-playbook -i ./hosts ./site-to-site-down.yml

site-2-multisite:
Changes must be done in hub.yml in oder to have the hub with the correct info for the spokes and in their specific file in the hosts_vars folder. How the hosts are organised can be seen in hosts.yml.
Create tunnels:
ansible-playbook -i ./hosts ./site-to-multisite-up.yml
Delete tunnels:
ansible-playbook -i ./hosts ./site-to-multisite-down.yml