# vagrant-bind-ansible-local
Build Bind Name Server (DNS) using Vagrant and Ansible Local Provisioner (suitable for windows)

The bind server was build using Ansible Bind Role 
1. https://github.com/bertvv/ansible-role-bind

It can be build using only 1 server - master without any slave

## Build the server
```
git clone https://github.com/riponbanik/vagrant-bind-ansible-local
cd vagrant-bind-ansible-local
vagrant up 
```

## Update the role
To update the Ansible Bind Role, use the commands below  -

```
1. cd vagrant-bind-ansible-local
2. ansible-galaxy install bertvv.bind -p roles
3. vagrant reload --provision
```

## When you're done, you can shut down the server using
```
vagrant halt
```


