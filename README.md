# ansibledeploys
Deployment of different artifacts using ansible with GPC, Azure and AWS

To use ansible in a windows machine, I recommend using WSL, execute powershell in admin mode and the use this command:  wsl --install
then, in the Linux terminal use the next commands: 
    sudo apt update
    sudo apt install ansible -y    
    ansible-galaxy collection install google.cloud --force
    sudo /usr/bin/python3 -m pip install google-auth google-auth-httplib2 google-api-python-client --break-system-packages
    gcloud iam service-accounts create ansible-service-account     --display-name "Ansible Service Account for camilo"
    gcloud projects add-iam-policy-binding maximal-zoo-295722     --member="serviceAccount:ansible-service-account@maximal-zoo-295722.iam.gserviceaccount.com"     --role="roles/storage.admin"    
    gcloud iam service-accounts keys create /mnt/c/Users/CAMILO/Documents/ansibledeploys/ansible-key.json     --iam-account=ansible-service-account@maximal-zoo-295722.iam.gserviceaccount.com
    export GOOGLE_APPLICATION_CREDENTIALS="/mnt/c/Users/CAMILO/Documents/ansibledeploys/ansible-key.json"

 ansible-playbook gcpBucket.yml
 ansible-playbook gcpDeleteBucket.yml

