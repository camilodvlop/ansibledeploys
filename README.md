# ansibledeploys
Deployment of different artifacts using ansible with GPC, Azure and AWS

To use ansible in a windows machine, I recommend using WSL (Windows subsystem for Linux), execute Powershell in admin mode and then use this command:  wsl --install
then, in the Linux terminal use the next commands: 
    sudo apt update
    #install ansible
    sudo apt install ansible -y    
    #install google collection for GCP (Google cloud plattform)
    ansible-galaxy collection install google.cloud --force
    # install dependencies, use ansible --version to check the path of the python version used by ansible in this case is:  /usr/bin/python3
    sudo /usr/bin/python3 -m pip install google-auth google-auth-httplib2 google-api-python-client --break-system-packages
    #create a service account in google cloud for ansible
    gcloud iam service-accounts create ansible-service-account     --display-name "Ansible Service Account for camilo"
    #add an iam policy
    gcloud projects add-iam-policy-binding maximal-zoo-295722     --member="serviceAccount:ansible-service-account@accountnameexample-1111.iam.gserviceaccount.com"     --role="roles/storage.admin"    
    #create a key for that IAM and store it on your local drive, WSL uses /mnt/c/ to find the disc C: in your local machine.
    gcloud iam service-accounts keys create /mnt/c/Users/NAMEUSERINWINDOWS/Documents/ansible/ansible-key.json     --iam-account=ansible-service-account@accountnameexample-1111.iam.gserviceaccount.com
    #export for use that key as a environment variable
    export GOOGLE_APPLICATION_CREDENTIALS="/mnt/c/Users/NAMEUSERINWINDOWS/Documents/ansible/ansible-key.json"

after that you can use the ansible command ansible-playbook to execute playbooks, make sure to execute the command in the same folder where the playbook is, you can cd tho the path, for instance: cd /mnt/c/Users/NAMEUSERINWINDOWS/Documents/ansible/playbooks
 ansible-playbook gcpBucket.yml
 #to delete the bucket use the playbook gcpDeleteBucket.yml
 ansible-playbook gcpDeleteBucket.yml

