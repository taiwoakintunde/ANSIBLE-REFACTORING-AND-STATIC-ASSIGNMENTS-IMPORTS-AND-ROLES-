## **Step 1 – Jenkins job enhancement** ##

>Note: Every new change in the codes creates a separate directory which is not very convenient when we want to run some commands from one place. Besides, it consumes space on Jenkins serves with each subsequent change. I will enhance it by introducing a new Jenkins project/job – we will require Copy Artifact plugin

Go to your Jenkins-Ansible server and create a new directory called ansible-config-artifact – we will store there all artifacts after each build.
```
sudo mkdir /home/ubuntu/ansible-config-artifact
```

![Alt text](images/1.PNG)

Change permissions to this directory, so Jenkins could save files there –
```
chmod -R 0777 /home/ubuntu/ansible-config-artifact
```
![Alt text](images/2.PNG)

Go to Jenkins web console -> Manage Jenkins -> Manage Plugins -> on Available tab search for Copy Artifact and install this plugin without restarting Jenkins

![Alt text](images/3.PNG)

Create a new Freestyle project (you have done it in Project 9) and name it save_artifacts.
![Alt text](images/4.PNG)

This project will be triggered by completion of existing ansible project. Configure it by enabling `Discard old builds`
Type 3 in `Max # of builds to keep` box, enable `Build after other projects are built` under Build Triggers and type 'ansible' under `Projects to watch` box
![Alt text](images/5.PNG)
![Alt text](images/6.PNG)

>The main idea of save_artifacts project is to save artifacts into /home/ubuntu/ansible-config-artifact directory. To achieve this, 

create a Build step and choose Copy artifacts from other project, specify ansible as a source project and /home/ubuntu/ansible-config-artifact as a target directory.
![Alt text](images/7.PNG)
![Alt text](images/8.PNG)








