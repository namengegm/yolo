# Configuring and provisining server using Ansible 
- Install vangrant
- Install ansible
- Confirm the version VBoxManage --version 
- Add VM do vagrant box add <box>
- Navigate to the project's folder i.e yolo 
- Vagrant box list   
- Innitialize vagrant within the folder,  run Vagrant box init generic/ubuntu
- Do vagrant up  - spin up the server 
- Check if vagrant box is running -  run vagrant status
- Get into the server  - vagrant ssh
- Exit 

# Separation of concerns using roles
Organize modules separately and refer them in playbook 

- Create a folder called roles
- Navigate to roles
- execute ansible-galaxy init <your_role_name>
- Navigate to task >main.yml and add executable commmands
-  Under playbook remove tasks and replace with roles
- List modules in preferred order of execution
- Run vagrant provision.

# Vagrantfile
## Add the following statement in the vagrant file to reference the playbook
### Config.vm.provision:ansible do |ansible| 
 ### ansible.playbook=“playbook.yaml”
### end 