
# ansible-auto-deploy
This will help for mass deplyment on all api and app boxes, this need to be run on each jumperbox in the respective cluster except for India where the machine is not in VPC.

The hosts file have host ips defined seperalty for each colo. The package list has been defined in the location roles directory, please find the directory structure shown below:

sreejith@eu2jumper1:~/ansible-auto-deploy$ tree .
.
├── eupkgdeploy.yml
├── hosts
├── indiapkgdeploy.yml
├── roles
│   ├── apipkgs
│   │   └── tasks
│   │       └── main.yml
│   ├── appserverpkgs
│   │   └── tasks
│   │       └── main.yml
│   └── update
│       └── tasks
│           └── main.yml
├── sgpkgdeploy.yml
└── uspkgdeploy.yml


The file named main.yml file have the details of packages listed as below:

---
  
- name: install packages
  apt: pkg={{item}} state=latest
  with_items:
    - ntp
    - cap-transfer-logs


If you want to add a new package named as sar, the yml can be written as shown below:


---
  
- name: install packages
  apt: pkg={{item}} state=latest
  with_items:
    - ntp
    - cap-transfer-logs
    - sar

In this way you can add many number of packages.

Finally the command used to execute this deployment is 

sreejith@jumper1:~/ansible-auto-deploy$ ansible-playbook -i hosts -K -k indiapkgdeploy.yml
SSH password: 
SUDO password[defaults to SSH password]: 

This will deploy the packages to the hosts defined on the hosts file. Siimilar way we can use the eupkgdeploy.yml, sgpkgdeploy.yml and uspkgdeploy.yml, but make sure you are running these yml on the respective jumper boxes.

Please do reach to me if you really have any doubts regarding this.

 

