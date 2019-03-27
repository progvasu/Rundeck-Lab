# Rundeck-Lab

## Installation Procedure

1. Install Java, if not already installed. <br/> 

    ```sudo apt install openjdk-8-jdk```

2. Get the latest Rundeck package from docs.rundeck.com/download/deb/ and install it. <br/>

    ```sudo dpkg -i {.deb file name}```

3. Start the Rundeck daemon <br/>

    ```sudo service rundeckd start ``` <br/>
    ```sudo service rundeckd status```
    
4. The web UI of the Rundeck instance can be accessed from localhost:4440. Login as: <br/>

    ```Username: admin``` <br/>
    ```Password: admin```

## Dispatching code onto the nodes




