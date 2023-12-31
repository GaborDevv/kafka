**RUNNING Clickstream Data Analysis Pipeline Using ksqlDB
- First I changed the maximum number of memory map areas a process may have (because of elasticsearch). (sudo sysctl -w vm.max_map_count=262144). 
- Then start running the start.sh script.
- It starts with running two containers and install kafka datagen connector which will produce data and kafka elasticsearch connector which will consume it.
- After these steps it will run the docker-compose yaml file to start all the necessery containers. 
![image](https://github.com/GaborDevv/kafka/assets/147967502/a2ac4004-9101-45e9-b88f-a2ee24399d57)

- Connect to the ksqlDB server and create source connectors for generating mock data:
![image](https://github.com/GaborDevv/kafka/assets/147967502/f717dd0f-4e25-416b-8808-c9aff1d6af3f)

- Create Stream tables in ksqlDB and tables for different types of analysis 
![image](https://github.com/GaborDevv/kafka/assets/147967502/23f5f1fd-3f0f-4f7b-ba47-fef4a86c47f9)
![image](https://github.com/GaborDevv/kafka/assets/147967502/d0f9e1d1-8bda-4a09-b979-71231b6e0229)


- After setting up elasticsearch mapping send ksqlDB tables to elasticsearch and grafana

![image](https://github.com/GaborDevv/kafka/assets/147967502/2b7c91c9-330c-4458-b706-686d7b4373cf)
![image](https://github.com/GaborDevv/kafka/assets/147967502/1d62e915-00e6-4b13-9fe8-387fdfd22194)

- Finally sessionize the data with the sessionize-data.sh script. Which will simulates user sessions. The script pauses the DATAGEN_CLICKSTREAM connector every 90 seconds for a 35 second period of inactivity which allows us to see different user sessions.

![image](https://github.com/GaborDevv/kafka/assets/147967502/9df9ade4-696f-42f2-80a5-ffd036c816e2)

Metrics: 

General website analytics, such as hit count and visitors:

![image](https://github.com/GaborDevv/kafka/assets/147967502/45c0d954-f2f6-4979-9ae9-52453f80cdd9)

Bandwidth use:
![image](https://github.com/GaborDevv/kafka/assets/147967502/29c7bc4f-b56b-4fd9-ac1a-435fcf88cfa2)

Mapping users to their IP address and actual location:

![image](https://github.com/GaborDevv/kafka/assets/147967502/b71213e9-345f-4401-9cfd-ef58d8a2fb97)

Detection of high-bandwidth user sessions (high bandwidth > 600k bytes/sec):

![image](https://github.com/GaborDevv/kafka/assets/147967502/29f8c993-5251-4139-9af4-3975bd9ac523)


Error code occurrence:

![image](https://github.com/GaborDevv/kafka/assets/147967502/f998f79a-3c26-4d44-a203-67465830a933)


Sessionization of resource hits to track user sessions:

![image](https://github.com/GaborDevv/kafka/assets/147967502/f0ed1027-ebbe-4bfb-91f0-40e207037cdb)
