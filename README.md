a) - This repo will help you to have a docker with jenkins, ansible and tearrform 
b) - If you want to parctice your self you just need to do below steps by cloging this repo.
c) - cd /Users/gangad
d) - git clone https://github.com/ganpirla/docker_jenkins_ansible_terraform.git
e) - cd /Users/gangad/docker_jenkins_ansible_terraform
f) - docker-compose build
g) - docker-compose up -d
h) - docker logs -f jenkins ( Copy the initialsecret to setup the jenkins)
i) - install needed jenkins plugins 
j) - now your jenkins docker is up with ansible and terraform in it.
k) - cd /Users/gangad/docker_jenkins_ansible_terraform/jenkins_home
l) - mkdir ansible
m) - cd  /Users/gangad/docker_jenkins_ansible_terraform/jenkins_home/ansible
n) - copy the private ssh key which was generated for the user remote_user in the above location
n) - vi hosts
[all:vars]

ansible_connection = ssh

[Test]

test1 ansible_host=remote_host ansible_user=remote_user ansible_private_key_file=/var/jenkins_home/ansible/remote-key
o) - thats it now ansiblr is ready - with this one docker for jenkins, ansible and terraform
p) - If you want to parctise more with anislbe playbook you can clone the another my repo https://github.com/ganpirla/ansible.git which ansible playbooks under /Users/gangad/docker_jenkins_ansible_terraform/jenkins_home/ansible