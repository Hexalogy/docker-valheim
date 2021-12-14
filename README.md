

# Docker-Valheim

## Step 1: Create a Linux Instance
To create a dedicated server, you must first create an instance. 
1. Sign up for an Amazon Lightsail account. 

Already have an account? Log in to your account

2. Open the Amazon Lightsail console. 

3. Click **Create instance**. 

4. Click **Change AWS Region and Availability Zone**. 
5. Under **Pick your instance image**, choose **Linux/Unix**, **OS Only**, **Ubuntu 20.04**
6. Choose the **4GB RAM** instance type or higher, you can get away with 2GB as long no more than 2 people connect to the server simultaneously. 

![enter image description here](https://user-images.githubusercontent.com/9726028/146091090-376da0ca-f092-4966-b998-7404ac0cda51.png)

## Step 2: Connect to your instance

1. Once your server is up, click the "**...**" icon and then click **Manage**

2. Add Networking rule to allow **UDP** protocol and allow port **2456-2458**

3. Click the **Connect** tab and click **Connect using SSH**.

## Step 3: Setup the Valheim server on your instance

1. You will run Valheim using docker. First, install docker:
```
curl -fsSL https://get.docker.com -o get-docker.sh 
sudo sh get-docker.sh 
sudo apt install docker-compose
```

2. Create the **docker-compose.yml** file. 

Replace **YOURSERVERNAME** and **ATLEAST5CHARACTERS** with a valid server name and password. Notice that this compose file also enables automatic updates and backups!

```bash
curl -o docker-compose.yml https://gist.githubusercontent.com/robzhu/a127a6bce1ea25b01d40efb57ad1c26e/raw/30a2927a901dd614a518319cfeaa63a6bd2648a4/gistfile1.txt

nano docker-compose.yml

#make your edits inside nano, then press CTRL+S, CTRL+X to save and quit
```

3. Bring up the server
```
sudo docker-compose up
```
use -d for detached mode

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

```
./valheim_server.x86_64 -name "[NAME]" -port 2456 -world "[WORLD]" -password "[PASSWORD]"
```

