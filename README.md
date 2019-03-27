# Rundeck-Lab

## Installation Procedure

1. Install Java, if not already installed. <br/> 

    ```sudo apt install openjdk-8-jdk```

2. Get the latest Rundeck package from [Rundeck Official Website](http://rundeck.org/download/deb) and install it. <br/>

    ```sudo dpkg -i {.deb file name}```

3. Start the Rundeck daemon <br/>

    ```sudo service rundeckd start ``` <br/>
    ```sudo service rundeckd status```
    
4. The web UI of the Rundeck instance can be accessed from localhost:4440. Login as: <br/>

    ```Username: admin``` <br/>
    ```Password: admin```

## Dispatching code onto the nodes

1. Create new project <br/>

    Fill in the Name and Description and let all other details be set in their default values and click Create.

2. Add Nodes/Clients to the Project <br/>

    Click on Edit for the Source file and mark the Writable option as checked and Save. <br/>
    You would now be able to edit the nodes file. <br/>
    Edit the nodes file. Add the following lines and save it. <br/>
    
   ```<node name="client" description="Client Node" tags=""``` <br/>
  ```hostname="Put Client Node IP Here" osArch="amd64" osFamily="unix"``` <br/>
  ```osName="Linux" osVersion="4.13.0-36-generic"``` <br/>
  ```username="Put Client Node User Here" sudo-command-enabled="true"``` <br/>
  ```sudo-password-option="option.sudoPassword"/>``` <br/>
  
3. Authenticated access to the clients <br/> 

    Rundeck uses ssh with ssh keys to securely access the client nodes. <br/>
    Run the following commands on your rundeck server. <br/>
    
    ```cd /var/lib/rundeck``` <br/>
    ```mkdir -p .ssh``` <br/>
    ```cd .ssh``` <br/>
    ```sudo ssh-keygen``` <br/>

    This will prompt you for a file name. Enter 'id_rsa'. Just press enter for the prompt "Enter passphrase". <br/>    
    You can now view the id_rsa.pub file using ```cat id_rsa.pub```. <br/>
    
    Copy the contents of id_rsa.pub file from the rundeck server and then perform the following operations in the client         node. <br/>
    
    ```cd ~``` <br/>
    ```mkdir -p .ssh``` <br/>
    ```cat >> ~/.ssh/authorized_keys``` <br/>
    ```<Paste the contents of id_rsa.pub file from the rundeck server>``` <br/>
    
    Verify that the contents were copied properly by viewing the contents of ~/.ssh/authorized_keys in the client node. <br/>
    
    ```cat ~/.ssh/authorized_keys``` <br/>

4. Verify the SSH connection <br/>

    Go to the ‘Commands’ tab of your project on the web UI of Rundeck server, enter the node name in the ‘Nodes’ input text entry and press ‘Search’. Then enter the shell command ‘echo test command’ in the ‘Command’ input text entry. Press ‘Run on 1 Node’ to execute the command. <br/>
    
5. Create a Job and Run it <br/>

    In the ‘Jobs’ tab, click on ‘Create a new Job’. Add any number of Steps in the Job workflow. Set Nodes to "Dispatch to Nodes" and Set the Node Filter if you want to filter which nodes to run this job on. Set the other options as required and click Create to save this job. <br/> 
    
    We can run the job manually using the ‘Run Job Now’ button or we can schedule the jobs to run at specified time intervals using ‘Run Job Later’. <br/>
    
    After the job is run, it gives the status of execution, time taken to complete the job and logs of all the job executions till now. This can be seen in the ‘Activity’ tab. <br/>







    

    



