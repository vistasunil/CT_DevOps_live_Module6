<div align="center">
<img src=https://static.wixstatic.com/media/1c706c_a5df0ad56f894928bf858a74ba744b32~mv2.png/v1/fit/w_2500,h_1330,al_c/1c706c_a5df0ad56f894928bf858a74ba744b32~mv2.png width="400" height="200">
 </div>

# <div align="center"> ANSIBLE ASSIGNMENT </p>

# <div align="center"> DevOps Instructor-led Training </div>

# <div align="right"> $`\textcolor{brown}{\text{Contact us: }}`$  &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; </div>

<div align="right"> T O A C C E L E R A T E Y O U R C A R E E R G R O W T H </div>

### <div align="right"> For questions and more details: </div>

<div align="right"> <img src=https://w7.pngwing.com/pngs/759/922/png-transparent-telephone-logo-iphone-telephone-call-smartphone-phone-electronics-text-trademark-thumbnail.png width="20" height="20"> +91 98712 72900 </div>

<div align="right"> <img src=https://pbs.twimg.com/profile_images/1450734615946219520/jmBHQRRa_400x400.jpg width="20" height="20"> https://www.thecloudtrain.com </div>

<div align="right"> <img src=https://icons.iconarchive.com/icons/martz90/circle/512/email-icon.png width="20" height="20"> support@thecloudtrain.com </div>

<div align="right"> <img src=https://png.pngtree.com/png-vector/20221018/ourmid/pngtree-whatsapp-icon-png-image_6315990.png width="20" height="20"> +91 98712 72900 </div>

#
</br>

## $`\textcolor{red}{\text{NOTE: USE UBUNTU 22.04 VIRTUAL MACHINES FOR ALL THE LABS}}`$


## Exercise 1: Ansible Module, Tasks, Play, Playbook and Conditionals

### Complete below tasks as part of this exercise:

* Create an Ansible playbook to perform below actions on slave nodes:
  * Install nginx first
  * Write the status of nginx installation as "nginx installed successfully!!" in a file /tmp/sw\_status.txt
  * Install apache now
  * Append the same file /tmp/sw\_status.txt with status of apache installation as "apache installed successfully!!"
  * Apache service must have failed to start because nginx is running on port 80. So, stop nginx service
  * Start apache service only if nginx is stopped

## Exercise 2: Ansible Roles

### Complete below tasks as part of this exercise:

* Create a role to perform below actions on slave nodes:
  * Install apache
  * Copy index.html from role's files directory to slaves /var/www/html directory
  * Copy apache2.conf from role's files directory to slaves /etc/apache2 directory
  * Restart apache service after copying new apache2.conf file using a notify
  * Create a handler in role's handler directory to get invoked by notify task. This handler task should restart apache service to reflect new conf changes
  * Create file apache2.conf in role's files directory using some existing apache2.conf reference. Make sure this file has right content, else service will fail to start.
  * Create index.html file in role's files directory with some html content.
  * Create a master playbook to call the roles and run all its tasks
  * Execute the playbook to apply all configuration changes
  * Access the html page that you copied browser using slave machine's public IP.

## Exercise 3: Case Study

**You are a Devops Engineer and the organization you are working on needs to set up two configuration management server groups. One for Apache another for Nginx. Being a Devops Engineer it is your task to deal with this configuration management issue. Let us see the tasks that you need to perform using Ansible.**

* Create two Server Groups. One for Apache and another for Nginx.
* Push two html files with their server information.
* Make sure that you don't forget to start the services once the installation is done. Also send post installation messages for both the server groups.
* Using Ansible Roles accomplish the above the tasks.
* Also, once the Apache server configuration is done you need to install Java on that server group using ansible role in a playbook.
