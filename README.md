# Configuring and provisining server using Ansible 
- Install vangrant
- Install ansible
- Create a folder
- Navigate to the folder 
- Vagrant box list  -- 
- Create a vagrant file  
- Vagrant box init generic/ubuntu
- Do vagrant up  - spin up the server 
- Check if vagrant box is running -  do vagrant status
- Get into the server  - vagrant ssh
- Exit 

# Separation of concerns using roles
Organize modules separately and refer them in playbook 

- Create a folder called roles
- Navigate to roles
- execute ansible-galaxy init <module name>
- Navigate to task >main.yml and add executable commmands
-  Under playbook remove tasks and replace with roles
- List modules in preferred order of execution
- Run vagrant provision.