# C9K IPsec Tunnel with AWS 

First things first you need to go to GCP and to generate credentials. There will be 2 keys: access and secret that need to be copied into localhost.yml file.
In hosts.yml make sure you have the correct ip address of the C9K that you want to connect to AWS.
In group_vars folder there is 1 file (switch.yml) that has the credentials to connect to C9K via SSH.
In host_vars there are 2 files. The localhost.yml file has all details that are needed to create/delete the AWS site. When the deployment of AWS is done a file will be generated called aws_site_details.json. In there you will find info that needs to replace the existent info in localhost.yml, in order to delete the AWS site. 
The onprem-site.yml has all the variables that C9K needs to connect to AWS site. It basically, creates 2 tunnels to AWS.
In all.yml file there are details for each tunnel: subnet and PSK.

To create AWS site:
Make sure in the localhost.yml file you have the right onprem site public IP address of the C9K.
ansible-playbook ./aws-site-up.yml
To delete AWS site:
Make sure that you changed the info from /host_vars/localhost.yml with aws-site-details.json
ansible-playbook ./aws-site-down.yml

To create C9K-AWS connection:
Make sure you have the correct data in the onprem-site.yml (public IP e.g.) 
ansible-playbook -i ./hosts ./site-to-site-up.yml

To delete C9K-AWS connection:
ansible-playbook -i ./hosts ./site-to-site-down.yml


Recommanded steps:
1. Create AWS site 
2. Create C9K tunnels
3. Delete C9K tunnels
4. Delete AWS site.