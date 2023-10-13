# C9K-GCP scenario

First things first you need to go to GCP and to generate credentials for a service account. It will generate a json file and it needs to be added to the current directory as gcp_auth.json.
Make sure the GCP Compute Engine API is enabled.
In hosts.yml make sure you have the correct ip address of the C9K that you want to connect to GCP.
In group_vars folder there is 1 file (switch.yml) that has the credentials to connect to C9K via SSH.
In host_vars there are 2 files. The localhost.yml file has all details that are needed to create/delete the GCP site. When the deployment of GCP is done a file will be generated called gcp_site_details.json. In there you will find info that needs to replace the existent info in localhost.yml, in order to delete the GCP site. 
The onprem-site.yml has all the variables that C9K needs to connect to GCP site. It basically, creates 2 tunnels to GCP.

To create GCP site:
Make sure in the localhost.yml file you have the right onprem site public IP address of the C9K.
ansible-playbook ./gcp-site-up.yml
To delete GCP site:
Make sure that you changed the info from /host_vars/localhost.yml with gcp-site-details.json
ansible-playbook ./gcp-site-down.yml

To create C9K-GCP connection:
Make sure you have the correct data in the onprem-site.yml (public IP e.g.) 
ansible-playbook -i ./hosts ./site-to-site-up.yml

To delete C9K-GCP connection:
ansible-playbook -i ./hosts ./site-to-site-down.yml


Recommanded steps:
1. Create GCP site 
2. Create C9K tunnels
3. Delete C9K tunnels
4. Delete GCP site.



