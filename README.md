
# Docker-Valheim

## Step 1: Create a Linux Instance
To create a dedicated server, you must first create an instance. 
1.1 — Sign up for an Amazon Lightsail account. 

Already have an account? Log in to your account

1.2  — Open the Amazon Lightsail console. 

1.3  — Click **Create instance**. 

1.4 — Click **Change AWS Region and Availability Zone**. 

## Step 2: Connect to your instance

1. Once your server is up, click the "**...**" icon and then click **Manage**

2. Add Networking rule to allow UDP protocol and allow port 2456-2458

3. Click the **Connect** tab and click **Connect using SSH**.

## Step 3: Setup the Valheim server on your instance

--


## Final Step 
`sudo docker-compose up -d && sleep 1 && sudo docker-compose logs -t -f`

So you can Ctrl+C and detach from the logs while the containers are still up.

To get access and run commands in that Docker container, use:

`sudo docker exec –it [CONTAINER_NAME] /bin/bash`

## How to import world

1. Stop the server if its running:

```sudo docker stop```

2. Upload the .db and .fw file to Dropbox, right-click and select Copy Dropbox link.

3. In your Lightsail instance, download these two files to your **./valheim/saves/worlds** directory

```
cd ./valheim/saves/worlds
wget https://www.dropbox.com/s/<FILE_ID>/YOURWORLD.db?dl=0 -O YOURWORLD.db
wget https://www.dropbox.com/s/<FILE_ID>/YOURWORLD.fwl?dl=0 -O YOURWORLD.fwl
```

4. Open docker-compose.yml and edit the WORLD property (line 12) to match the name of your .db/.fwl files. 

5. Open **./valheim/server/start-server.sh** and edit the name of the World so it match.

