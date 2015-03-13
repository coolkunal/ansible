##### Issue Type:

Bug Report

##### Ansible Version:
Ansbile Version 1.8.4

ansible 1.8.4

##### Environment:

Running Ansible Playbook from -Red Hat Enterprise Linux Server release 5.5 (Tikanga) 
Managing os -Rhel 6.4(Santiago)(remote server)

##### Summary:

I am running synchrnoize module in my playbook to copy of the tar file to remote server and i have observed that synchrnoize.py module of ansible is failing for this operation due to rsync output format issue.
Error which i am getting after running playbook is:

failed: [ip -> 127.0.0.1] => {"cmd": "rsync --delay-updates -FF --compress --archive --rsh 'ssh -S none -o StrictHostKeyChecking=no' --out-format='<>%i %n%L' \"/prd/file.tar.gz/roles/server/files/abc.tar.tgz\" \"root@remoteip:/tmp\"", "failed": true, "rc": 1}
msg: rsync: --out-format=<>%i %n%L: unknown option
rsync error: syntax or usage error (code 1) at main.c(1231) [client=2.6.8]

FATAL: all hosts have already failed -- aborting

I am using synchronize module of ansible for copying operation which is failing since rsync: --out-format=<>%i %n%L: unknown option..
I have also changed synchronize.py module by adding some lines of code to avoid the above prblem..
Please look into this as for rhel 5.5 its not working

##### Steps To Reproduce:

Playbook example:
The below tasks is added in one of the roles .So when I am running playbook the playbook fails at this point .
Problem is the rsync which is used by syncroize is adding  --out-format=<>%i %n%L which is unknown option.

  - name: Copying the build on to the remote server
   synchronize: src={build_name}}.tgz dest=/tmp


##### Expected Results:
Expected result - build should get copied to path specified in remote server

##### Actual Results:

Actual output:

failed: [ip -> 127.0.0.1] => {"cmd": "rsync --delay-updates -FF --compress --archive --rsh 'ssh -S none -o StrictHostKeyChecking=no' --out-format='<>%i %n%L' \"/prd/file.tar.gz/roles/server/files/abc.tar.tgz\" \"root@remoteip:/tmp\"", "failed": true, "rc": 1}
msg: rsync: --out-format=<>%i %n%L: unknown option

FATAL: all hosts have already failed -- aborting


