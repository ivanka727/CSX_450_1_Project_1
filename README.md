# CSX_450_1_Project_1
## I. SSH keys & Amazon EC2
1. Open your browser 
2. Go to Amazon Web Services (https://aws.amazon.com/console/) 
3. Create an AWS account 
4. Sign in AWS 
5. Select “EC2” under “Compute” in All services list 
6. Check “Key Pairs” under “Resources” panel, if it shows “0 Key Pairs”, please set up a one locally.
7. Open your Bash shell 
8. Type “ssh-keygen” 
9. Hit “enter” 
10. Save it into the default location without adding a passphrase 
11. Hit “enter” twice, you’ll see 2 files “id_rsa” and “id_rsa.pub” saved in “ssh” folder. 
12. Retrieve the content from “id_rsa.pub”
13. Type “cat ~/.ssh/id_rsa.pub”, hit “enter”
14. You’ll see the key in the shell
15. Copy the key.
16. Go back to AWS
17. Click “Key Pairs”
18. Click “Import Key Pair”
19. Name the Key Pair
20. Paste the key to “Public Key Contents” 
21. Click “Import”. (See below screenshot)

## II. Security Groups
1. Go back to EC2 Dashboard
2. Select “ Security Groups”
3. “Create Security Group” 
4. Click “Add Rule”
5. Select “SSH” under “Type” and select “anywhere” under “Source” 
6. Add another rule, select “HTTP” under “Type” and select “anywhere” under “Source”.
7. Name the Security Group --- Add “Description” --- Click “Create”. (See below screenshot)

## III. AWS Operating System
1. Go back to AWS Dashboard
2. “Launch Instance”
3. Choose Amazon Machine Image, select “Ubuntu Server 16.04 LTS (HVM), SSD Volume Type - ami-1ee65166”.
4. Choose an instance type, select “t2.micro (free tier eligible)”
5. Click “Next: Configure Instance Details”.
6. Use default settings and click “Next: Add storage”.
7. Change “Size (GiB) to “30” which is free to customers and click “Next: Configure Security Group”.
8. Select an existing security group (the one you just created), make sure port 22 and 80 are there.
9. Review and Launch, you can disregard the warning. If everything looks good, then click “Launch”.
10. Choose an existing key pair, select the one you just created
11. Launch Instances and view Instances.
12. Name the instance, check the inbound rules and make sure ports 80 and 22 are there. You’ll also see a generated IP address.

## IV. Docker Installation
1. Copy the public IP Address from the instance.
2. Go back to Bash Shell
3. Type “ssh ubuntu@IP address”
4. Click “enter”, then connect (type “yes”)
5. Type “curl -sSL https://get.docker.com | sh” to start downloading and installing docker. 
6. Add our user to the docker group, copy and paste the text from above red box and run it. Type “exit” to logout and log back in. Then we’ll have docker installed.

## V. Obtaining the correct Docker image
1. Launch Jupyter notebook server
2. Verify the docker works fine
3. Type “docker pull jupyter/datascience-notebook” to pull the image.
4. Type “docker images” to verify the image has been pulled out correctly.
5. To give the name a shorter tag, type “docker tag image ID dsnb” to tag it as “dsnb”.

## VI. Running the correct Docker image as a container
1. Run this image by typing “docker run -v /home/ubuntu:/home/jovyan -p 80:8888 -d dsnb” to obtain the container ID. 
2. Type “docker ps” to see the container.

## VII. Jupyter notebook security concerns
1. Open the browser, put IP address in, connect with Jupyter notebook server.
2. Go back to Bash shell, run “docker exec container ID jupyter notebook list” to get the token
3. Copy the token and put it back into the browser “Password or token” part, then login. 

## VIII. Diagram
![my image](https://github.com/lssnadia/CSX_450_1_Project_1/blob/master/Launch%20Jupyter%20Diagram.001.jpeg)

## IX. A detailed budget of the costs of running a Jupyter Data Science Notebook Server for three months using at least three different kinds of EC 2 instances.
- Assume we’re using 30GB storage with Linux per month in Oregon Region.
 1. Instance Type 1: t2.small, usage rate is $0.023 per hour, data transfer rate is $0.09/GB. Total rate for 3 months = rate/hour * hours/day * days/month * total months + data transfer rate * 30GB = $0.023 * 24 * 30 * 3 + $0.09 * 30 = $52.38
 2. Instance Type 2: t2.medium, usage rate is $0.0464 per hour, data transfer rate is $0.09/GB. Total rate for 3 months = rate/hour * hours/day * days/month * total months + data transfer rate * 30GB = $0.0464 * 24 * 30 * 3 + $0.09 * 30 = $102.924
 3. Instance Type 3: m5.large, usage rate is $0.096 per hour, data transfer rate is $0.09/GB. Total rate for 3 months = rate/hour * hours/day * days/month * total months + data transfer rate * 30GB = $0.096 * 24 * 30 * 3 + $0.09 * 30 = $210.06
- Total cost = Instance type 1 cost + Instance type 2 cost + Instance type 3 cost = $52.38+$102.924+$210.06 = $365.364
	
