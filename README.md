# Docker-Valheim

## Step 1: Create a Linux Instance
To create a dedicated server, you must first create an instance. 
1.1 — Sign up for an Amazon Lightsail account. 

Already have an account? Log in to your account

1.2  — Open the Amazon Lightsail console. 

1.3  — Click Create instance. 

1.4 — Click Change AWS Region and Availability Zone. 

## Step 2:

## Final Step 
`sudo docker-compose up -d && sleep 1 && sudo docker-compose logs -t -f`

So you can Ctrl+C and detach from the logs while the containers are still up.

To get access and run commands in that Docker container, use:

`sudo docker exec –it [CONTAINER_NAME] /bin/bash`
