## Prerequisites ##

Docker and docker compose should be installed in your VM.

## Procedure ##

a) - This repo will help you to have a docker with jenkins, ansible and tearrform 
b) - If you want to parctice your self you just need to do below steps by cloging this repo.
c) - cd /Users/gangad
d) - git clone https://github.com/ganpirla/docker_jenkins_ansible_terraform.git
e) - cd /Users/gangad/docker_jenkins_ansible_terraform/centos7
f) - ssh-keygen -f remote-key (do not enter any input keep press ENTER key) 
g) - ls -lart  ( once done  you should see 2 files with ssh keys -  remote-key, remote-key.pub )
h) - Copy those 2 ssh files into server1 through server10 respective folders
i) - docker-compose build
j) - docker-compose up -d
k) - docker logs -f jenkins ( Copy the jenkins initial secret to setup and to complete the jenkins)
l) - install needed jenkins plugins along with ansible and terraform plugins.
m) - now your jenkins docker is up with ansible and terraform in it and also server1 to server10 vms for testing.
n) - cd  /Users/gangad/docker_jenkins_ansible_terraform/jenkins_home/ansible
o) - copy the private ssh key remote-key which was generated for the user remote_user in the above location
p) - thats it now ansible is ready. 
q) - If you want to parctise more with anislbe playbook you can clone the another my repo https://github.com/ganpirla/ansible.git which ansible playbooks under /Users/gangad/docker_jenkins_ansible_terraform/jenkins_home/ansible

## connection test ##

Below you can see jenkins VM is able to access server1 through server10 with private key and able to run all the ansible commands and playbooks. Also the same commands can be executed form jenkins url with projects by using the execute shell block 

gangad@Pirlas-MacBook-Air jenkins_home % docker container exec -it jenkins bash
jenkins@ac06a64bdf03:/$ cd /var/jenkins_home/ansible/
jenkins@ac06a64bdf03:~/ansible$ 
jenkins@ac06a64bdf03:~/ansible$ cat hosts 
[all:vars]

ansible_connection = ssh

[TEST]

test1 ansible_host=remote_host ansible_user=remote_user ansible_private_key_file=/var/jenkins_home/ansible/remote-key

[PROD]

prod1 ansible_host=server1 ansible_user=remote_user ansible_private_key_file=/var/jenkins_home/ansible/remote-key
prod2 ansible_host=server2 ansible_user=remote_user ansible_private_key_file=/var/jenkins_home/ansible/remote-key
prod3 ansible_host=server3 ansible_user=remote_user ansible_private_key_file=/var/jenkins_home/ansible/remote-key

[DEV]

dev1 ansible_host=server4 ansible_user=remote_user ansible_private_key_file=/var/jenkins_home/ansible/remote-key
dev2 ansible_host=server5 ansible_user=remote_user ansible_private_key_file=/var/jenkins_home/ansible/remote-key
dev3 ansible_host=server6 ansible_user=remote_user ansible_private_key_file=/var/jenkins_home/ansible/remote-key

[QA]

qa1 ansible_host=server7 ansible_user=remote_user ansible_private_key_file=/var/jenkins_home/ansible/remote-key
qa2 ansible_host=server8 ansible_user=remote_user ansible_private_key_file=/var/jenkins_home/ansible/remote-key
qa3 ansible_host=server9 ansible_user=remote_user ansible_private_key_file=/var/jenkins_home/ansible/remote-key
qa4 ansible_host=server10 ansible_user=remote_user ansible_private_key_file=/var/jenkins_home/ansible/remote-key
jenkins@ac06a64bdf03:~/ansible$ 
jenkins@ac06a64bdf03:~/ansible$ 
jenkins@ac06a64bdf03:~/ansible$ ssh -i remote-key remote_user@server1
Last login: Mon Dec 12 08:14:26 2022 from jenkins.devops_net
[remote_user@aa03b7fff847 ~]$ 
[remote_user@aa03b7fff847 ~]$ exit
logout
Connection to server1 closed.
jenkins@ac06a64bdf03:~/ansible$ 
jenkins@ac06a64bdf03:~/ansible$ 
jenkins@ac06a64bdf03:~/ansible$ ssh -i remote-key remote_user@server2
Last login: Mon Dec 12 08:14:26 2022 from jenkins.devops_net
[remote_user@0603aabe6e61 ~]$ 
[remote_user@0603aabe6e61 ~]$ 
[remote_user@0603aabe6e61 ~]$ 
[remote_user@0603aabe6e61 ~]$ exit
logout
Connection to server2 closed.
jenkins@ac06a64bdf03:~/ansible$ 
jenkins@ac06a64bdf03:~/ansible$ ssh -i remote-key remote_user@server3
Last login: Mon Dec 12 08:14:26 2022 from jenkins.devops_net
[remote_user@b05dbe97ce05 ~]$ 
[remote_user@b05dbe97ce05 ~]$ 
[remote_user@b05dbe97ce05 ~]$ exit
logout
Connection to server3 closed.
jenkins@ac06a64bdf03:~/ansible$ 


jenkins@ac06a64bdf03:~/ansible/playbooks$ ansible -i ../hosts -m ping PROD
prod2 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
prod1 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
prod3 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
jenkins@ac06a64bdf03:~/ansible/playbooks$ 
jenkins@ac06a64bdf03:~/ansible/playbooks$ 
jenkins@ac06a64bdf03:~/ansible/playbooks$ ansible -i ../hosts -m ping TEST
test1 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
jenkins@ac06a64bdf03:~/ansible/playbooks$ 
jenkins@ac06a64bdf03:~/ansible/playbooks$ ansible -i ../hosts -m ping DEV
dev2 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
dev3 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
dev1 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
jenkins@ac06a64bdf03:~/ansible/playbooks$ 
jenkins@ac06a64bdf03:~/ansible/playbooks$ ansible -i ../hosts -m ping QA
qa1 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
qa2 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
qa4 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
qa3 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
jenkins@ac06a64bdf03:~/ansible/playbooks$ 



jenkins@ac06a64bdf03:~/ansible/playbooks$ ansible-playbook -i ../hosts command_run_shell.yml 

PLAY [all] ***************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************
ok: [prod1]
ok: [test1]
ok: [dev1]
ok: [prod3]
ok: [prod2]
ok: [qa2]
ok: [dev2]
ok: [qa1]
ok: [dev3]
ok: [qa3]
ok: [qa4]

TASK [Running a Linux command in shell] **********************************************************************************************************************
changed: [test1]
changed: [prod3]
changed: [prod1]
changed: [prod2]
changed: [dev1]
changed: [dev3]
changed: [qa1]
changed: [dev2]
changed: [qa3]
changed: [qa2]
changed: [qa4]

TASK [Displaying the df command output] **********************************************************************************************************************
ok: [test1] => {
    "msg": "Filesystem     1K-blocks    Used Available Use% Mounted on\noverlay         61202244 5875176  52185744  11% /\ntmpfs              65536       0     65536   0% /dev\nshm                65536       0     65536   0% /dev/shm\n/dev/vda1       61202244 5875176  52185744  11% /etc/hosts\ntmpfs            2013396       0   2013396   0% /sys/firmware"
}
ok: [prod1] => {
    "msg": "Filesystem     1K-blocks    Used Available Use% Mounted on\noverlay         61202244 5874704  52186216  11% /\ntmpfs              65536       0     65536   0% /dev\nshm                65536       0     65536   0% /dev/shm\n/dev/vda1       61202244 5874704  52186216  11% /etc/hosts\ntmpfs            2013396       0   2013396   0% /sys/firmware"
}
ok: [prod2] => {
    "msg": "Filesystem     1K-blocks    Used Available Use% Mounted on\noverlay         61202244 5874476  52186444  11% /\ntmpfs              65536       0     65536   0% /dev\nshm                65536       0     65536   0% /dev/shm\n/dev/vda1       61202244 5874476  52186444  11% /etc/hosts\ntmpfs            2013396       0   2013396   0% /sys/firmware"
}
ok: [prod3] => {
    "msg": "Filesystem     1K-blocks    Used Available Use% Mounted on\noverlay         61202244 5875076  52185844  11% /\ntmpfs              65536       0     65536   0% /dev\nshm                65536       0     65536   0% /dev/shm\n/dev/vda1       61202244 5875076  52185844  11% /etc/hosts\ntmpfs            2013396       0   2013396   0% /sys/firmware"
}
ok: [dev1] => {
    "msg": "Filesystem     1K-blocks    Used Available Use% Mounted on\noverlay         61202244 5874640  52186280  11% /\ntmpfs              65536       0     65536   0% /dev\nshm                65536       0     65536   0% /dev/shm\n/dev/vda1       61202244 5874640  52186280  11% /etc/hosts\ntmpfs            2013396       0   2013396   0% /sys/firmware"
}
ok: [dev2] => {
    "msg": "Filesystem     1K-blocks    Used Available Use% Mounted on\noverlay         61202244 5874840  52186080  11% /\ntmpfs              65536       0     65536   0% /dev\nshm                65536       0     65536   0% /dev/shm\n/dev/vda1       61202244 5874840  52186080  11% /etc/hosts\ntmpfs            2013396       0   2013396   0% /sys/firmware"
}
ok: [dev3] => {
    "msg": "Filesystem     1K-blocks    Used Available Use% Mounted on\noverlay         61202244 5875076  52185844  11% /\ntmpfs              65536       0     65536   0% /dev\nshm                65536       0     65536   0% /dev/shm\n/dev/vda1       61202244 5875076  52185844  11% /etc/hosts\ntmpfs            2013396       0   2013396   0% /sys/firmware"
}
ok: [qa1] => {
    "msg": "Filesystem     1K-blocks    Used Available Use% Mounted on\noverlay         61202244 5875176  52185744  11% /\ntmpfs              65536       0     65536   0% /dev\nshm                65536       0     65536   0% /dev/shm\n/dev/vda1       61202244 5875176  52185744  11% /etc/hosts\ntmpfs            2013396       0   2013396   0% /sys/firmware"
}
ok: [qa2] => {
    "msg": "Filesystem     1K-blocks    Used Available Use% Mounted on\noverlay         61202244 5874468  52186452  11% /\ntmpfs              65536       0     65536   0% /dev\nshm                65536       0     65536   0% /dev/shm\n/dev/vda1       61202244 5874468  52186452  11% /etc/hosts\ntmpfs            2013396       0   2013396   0% /sys/firmware"
}
ok: [qa3] => {
    "msg": "Filesystem     1K-blocks    Used Available Use% Mounted on\noverlay         61202244 5874604  52186316  11% /\ntmpfs              65536       0     65536   0% /dev\nshm                65536       0     65536   0% /dev/shm\n/dev/vda1       61202244 5874604  52186316  11% /etc/hosts\ntmpfs            2013396       0   2013396   0% /sys/firmware"
}
ok: [qa4] => {
    "msg": "Filesystem     1K-blocks    Used Available Use% Mounted on\noverlay         61202244 5874232  52186688  11% /\ntmpfs              65536       0     65536   0% /dev\nshm                65536       0     65536   0% /dev/shm\n/dev/vda1       61202244 5874232  52186688  11% /etc/hosts\ntmpfs            2013396       0   2013396   0% /sys/firmware"
}

PLAY RECAP ***************************************************************************************************************************************************
dev1                       : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
dev2                       : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
dev3                       : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
prod1                      : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
prod2                      : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
prod3                      : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
qa1                        : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
qa2                        : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
qa3                        : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
qa4                        : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
test1                      : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

jenkins@ac06a64bdf03:~/ansible/playbooks$ 

