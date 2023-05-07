<div align="center">
<img src=https://static.wixstatic.com/media/1c706c_a5df0ad56f894928bf858a74ba744b32~mv2.png/v1/fit/w_2500,h_1330,al_c/1c706c_a5df0ad56f894928bf858a74ba744b32~mv2.png width="400" height="200">
 </div>

# <div align="center"> ANSIBLE </p>

# <div align="center"> DevOps Instructor-led Training </div>

<br />

<br />

<br />

<br />

# $${\color{brown} &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; Contact&emsp;us: &emsp;&emsp;&emsp; }$$

<div align="right"> T O A C C E L E R A T E Y O U R C A R E E R G R O W T H </div>

### <div align="right"> For questions and more details: </div>

<div align="right"> <img src=https://w7.pngwing.com/pngs/759/922/png-transparent-telephone-logo-iphone-telephone-call-smartphone-phone-electronics-text-trademark-thumbnail.png width="20" height="20"> +91 98712 72900 </div>

<div align="right"> <img src=https://pbs.twimg.com/profile_images/1450734615946219520/jmBHQRRa_400x400.jpg width="20" height="20"> https://www.thecloudtrain.com </div>

<div align="right"> <img src=https://icons.iconarchive.com/icons/martz90/circle/512/email-icon.png width="20" height="20"> support@thecloudtrain.com </div>

<div align="right"> <img src=https://png.pngtree.com/png-vector/20221018/ourmid/pngtree-whatsapp-icon-png-image_6315990.png width="20" height="20"> +91 98712 72900 </div>

## ANSIBLE HANDS-ON

### Install Ansible

[**Ansible Installation officical document**](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-ubuntu)

```
sudo apt update
sudo apt install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

![image](https://user-images.githubusercontent.com/37858762/236036904-9f71c528-8579-4f99-8f88-fd8aec54f826.png)

**Ansible hands-on documentation has been divided into 3 segments.**

* A. Creating Ansible Playbook 
* B. Creating Ansible Roles 
* C. Using Ansible Roles in Playbook 

### Prerequisites

* Ansible needs to be installed in master. 
* Connection between Master and Host needs to be set through ssh. For more information refer to the Ansible Installation Documentation.

## A) Creating Ansible Playbook

This playbook consists of two plays with following tasks:

- Play 1: Execute a command in host1, Execute a script in host1
- Play 2: Execute a script in host2, Install nginx in host2

### Step 1: Create the .yml file.

`sudo vim <playbookname>`

### Step 2: Add the following content in the .yml file.

```
---
- hosts: host1
  become: yes
  name: Play 1
  tasks:
    - name: Execute command ‘Date’
      command: date
    - name: Execute script on server
      script: test_script.sh
- hosts: host2
  name: Play 2
  become: yes
  tasks:
    - name: Execute script on server
      script: test_script.sh
    - name: Install nginx
      apt: name=nginx state=latest
```

![image](https://user-images.githubusercontent.com/37858762/236037045-83e67b55-851e-4a40-8ea3-99f2b3a137e5.png)

### Step 3: Now to be able to perform **Execute script on server** task we need to have the **.sh** file (unix (linux) _shell_ executables _files_) in master machine. Create test\_script.sh file as shown.

`sudo vim <file_name>`

![image](https://user-images.githubusercontent.com/37858762/236037114-ef33af39-9e01-47cf-82b2-cfca0582db73.png)

### Step 4: Before executing the playbook that we just created we need to have to check for syntax errors.

`ansible-playbook <playbook> --syntax-check`

![image](https://user-images.githubusercontent.com/37858762/236037186-0b0f3fb7-73c7-4a16-89f1-d79a5613d18d.png)

This means our playbook is syntax error free. Let us move ahead and execute the playbook.

### Step 5: To execute the playbook use the following command.

`ansible-playbook <playbook>`

![image](https://user-images.githubusercontent.com/37858762/236037260-1118a711-abaf-4ce7-bbb3-e15f6498cf79.png)

Great! We have successfully created our very first Ansible playbook.

Remember that using playbook we can run the same command repeatedly, but if everything was configured on the first run, then all subsequent runs make no changes.

### Final playbook

```
---
- hosts: "{{ server }}"
  become: yes
  name: Play 1
  gather_facts: yes
  vars:
    a: "hello"
    b: "world"
  tasks:
    - name: Execute command ‘Date’
      shell: date && hostname && echo "{{ a }}"
      register: date_out
      ignore_errors: yes

    - name: Execute script on server
      script: test_script.sh

    - debug:
        msg: "output: {{ item }}"
      when: date_out.rc == 0
      with_items: "{{date_out.stdout_lines }}"

    - debug:
        var: date_out.stdout_lines

    - name: install tomcat
      yum:
        name: tomcat9
        state: latest
      when: ansible_distribution == "RHEL"

    - name: install tomcat
      apt:
        name: tomcat9
        state: latest
        update_cache: yes
      when: ansible_distribution == "Ubuntu"

    - debug:
        msg: "{{ item[0]}}: {{ item.1 }}"
      with_together:
      - ["date_output","server","print"]
      - "{{date_out.stdout_lines }}"

    - debug:
        msg: "{{ item[0]}}: {{ item.1 }}"
      with_nested:
      - ["a", "b", "c"]
      - [1,2,3] 
```      

## B) Creating Ansible Roles

### Step 1: Ansible roles should be written inside "_/etc/ansible/roles/_ ". Use the following command to create one Ansible role.

`ansible-galaxy init <role name> --offline`

![image](https://user-images.githubusercontent.com/37858762/236037308-a073acca-7e18-4882-9b3e-8df4b2739086.png)

### Step 2: Install tree package using sudo apt install tree. Use tree command to view structure of the role

`sudo apt install tree`

![image](https://user-images.githubusercontent.com/37858762/236037339-a4a12c4f-ca00-4e11-8904-6f2da05149ae.png)

Now let us see the structure of the role that we just created using the following command.

`tree <role name>`

![image](https://user-images.githubusercontent.com/37858762/236037370-c1a3967d-7fb5-4b8e-82c0-36d48be553d5.png)

Now we are ready to create the tasks that our roles are supposed to perform.

### Step 3: Go inside _tasks_ folder inside _apache_ directory. Edit _main.yml_ using the following command. Make changes as shown. Save and then exit.

`sudo vim main.yml`

Now we will divide the tasks to be performed into three categories. Install, configure and services. We will create three different .yml files to reduce the complexity. Include those separate task files in the main.yml file as shown.

```
---

# tasks file for apache

- include: install.yml
- include: configure.yml
- include: service.yml
```

![image](https://user-images.githubusercontent.com/37858762/236037410-33d0d60b-d2e8-450c-9732-9327535077af.png)

Remember that order of the list in yml file matters. So here install.yml gets executed first, then configure.yml and then service.yml.

### Step 4: Now inside _task_ folder, create _install.yml_ and add the installation tasks to be performed as shown below.

`sudo vim install.yml`

We will install the latest version of apache2 in the remote machine with the help of apt module as shown below.

```
---
- name: install apache2
  apt: name=apache2 update_cache=yes state=latest
```

![image](https://user-images.githubusercontent.com/37858762/236037454-1886c85c-4cfd-40a9-a873-89594befba09.png)

### Step 5: Then create _configure.yml_ and add the required configurations that need to be performed on remote machine as shown below.

`sudo vim configure.yml`

We will configure apache2.conf file in the remote machine and also, we will restart the apache2 service. Then we will send one file from _/etc/ansible/roles/apache/files_ folder to the remote machine. The destination path has been set to /home/ubuntu/ as shown.

```
---
#configure apache2.conf and send copy.html file
  - name: apache2.conf file
    copy: src=apache2.conf dest=/etc/apache2/
    notify:
    - restart apache2 service
    
  - name: send copy.html file
    copy: src=index.html dest=/var/www/html/
```

![image](https://user-images.githubusercontent.com/37858762/236037492-588bfd17-afaa-4cf8-8ce0-3d54d7d21ce1.png)

### Step 6: Again, inside _task_ folder, create _service.yml_ and add the required configurations that need to be performed on remote machine as shown below.

`sudo vim service.yml`

We will configure apache2.conf file in the remote machine

```
---
- name: starting apache2 service
  service: name=apache2 state=started
```

![image](https://user-images.githubusercontent.com/37858762/236037589-21139414-f0ab-4467-b0f5-1aca30266997.png)

### Step 7: Now, Now go inside files. Store the files that needs to be pushed to the remote machine. Copy the apache2.conf file from _/etc/apache2_ directory to _/etc/ansible/roles/apache\_demo/files_ and create the html file.

`cp /etc/apache2/apache2.conf <roles_folder>/<role_name>/files`

Create one html file as well. My dummy html file looks like this.

```
<html>
<title> Demo File </title>
  <body> <h1> WELCOME to ANSIBLE DEMO </h1> </body>
</html>
```

![image](https://user-images.githubusercontent.com/37858762/236037631-292776fc-df28-4a27-b984-c8a0c227ea38.png)

Check whether our files are ready or not by using the following command.

`ls -ltr`

![image](https://user-images.githubusercontent.com/37858762/236037657-3508cbd2-994d-4de3-9ee7-844e25003adb.png)

### Step 8: Go inside handlers and add the action that needs to be performed after _notify_ from _configure.yml_ is executed. Use the following two commands.

`cd <roles_folder>/<role_name>/handlers/`

`sudo vim main.yml`

```
---

# handlers file for apache

- name: restart apache2 service
  service: name=apache2 state=restarted
```

![image](https://user-images.githubusercontent.com/37858762/236037682-92d646bd-aaf0-4428-91cc-3a44247528ce.png)

Remember that notify name and handler name should match.

![image](https://user-images.githubusercontent.com/37858762/236037702-76859c39-7c86-4ed9-bea8-f083a0bb043a.png)

![image](https://user-images.githubusercontent.com/37858762/236037744-7de32bd0-04f9-4666-a80a-a71e030d25e0.png)


### Step 9: Go inside meta and add information related to the role.

`cd <roles_folder>/handlers/`

`sudo vim main.yml`

Add author information, role descriptions, company information etc. as shown below.

![image](https://user-images.githubusercontent.com/37858762/236037776-578a28ee-5039-4c40-a3b5-ec12756f248e.png)

### Step 10: Create one top level _.yml_ file where we can add hosts and roles to be executed. Execute apache role on the hosts that is under the group name servers, added in the inventory file _/etc/ansible/hosts_

`sudo vim masterplay.yml`

For more than one hosts following commands can be used.

```
---
  - hosts: servers
    become: yes
    roles:
    - apache_demo 
```

![image](https://user-images.githubusercontent.com/37858762/236037812-eec4dda2-e540-4198-bb35-61baf1b83aa1.png)

### Step 11: Before we execute our top level yml file we will check for syntax errors.

`ansible-playbook <filename.yml> --syntax-check`

![image](https://user-images.githubusercontent.com/37858762/236038040-8532261e-de8b-448e-99d6-453549de1705.png)

### Step 12: Execute the top level *.yml* file

`ansible-playbook <filename.yml>`

The output looks like this.

![image](https://user-images.githubusercontent.com/37858762/236038091-843a350e-f743-4433-9026-ebab3a24bbf9.png)

![image](https://user-images.githubusercontent.com/37858762/236038120-0cafc000-6fcc-4bcf-8cd5-5327b812cd63.png)

Congratulations! You have successfully created Ansible Role.

Now let us see how to use this Ansible role that we've just created along with other tasks in a Ansible Playbook.

## C) Using Ansible Roles in Playbook

### Step 1: To use ansible roles along with other tasks in playbook use _import\_role_ and _include\_role._ Create one playbook called to execute on the remote machines along with two _debug_ tasks before and after _apache role_.

`sudo vim <playbook name>`

Add the following **.yml** file as shown.

```
---
  - hosts: servers
    become: yes
    tasks:
    - debug:
        msg: "before we run our role"
    - import_role:
        name: apache
    - include_role:
        name: apache
    - debug:
        msg: "after we ran our role"
```

### Step 2: Check for syntax error and execute the playbook with roles.

`ansible-playbook <playbookname> --syntax-check`

![image](https://user-images.githubusercontent.com/37858762/236038192-d0b62ea2-9b4b-4ee5-874e-dc21df6e9aa8.png)

### Step 3: Check for syntax error and execute the playbook with roles.

`ansible-playbook <playbookname>`

![image](https://user-images.githubusercontent.com/37858762/236038239-c6f261e8-32e3-4e54-8984-71302c45b8fd.png)

**Congratulations!** You have successfully integrated Ansible roles with Ansible playbook.

## Ansible Vault

[Document for Ansible Vault](https://www.redhat.com/sysadmin/introduction-ansible-vault)
