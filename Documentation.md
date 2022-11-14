# Open Horizon Documentation
The purpose of this repository is to document my experience working on the Open Horizon project and what I have learned. Initially, I believed that Open Horizon was one
big project with a single repository; however, it turned out to be one community with multiple individual repositories that all had issues. Because of this style, there
was not much guidance or direction and I just picked from the plethora of repositories that had issues. Some of the issues within these repositories were extremely simple
and some were difficult and required more experience. My original plan was to start with the simple issues and then work my way up to the more difficult issues. Here
are the issues that I have accomplished so far.

## Adding Shields to README
These types of issues are the most common ones that I have seen across all of the repositories. They are all labeled "good first issue", which is the reason as to why I began working on these types of questions first.

<img width="437" alt="Screenshot 2022-11-08 075206" src="https://user-images.githubusercontent.com/62410569/200573725-9c0cd043-8fbd-400b-aa56-5758b4d18b5d.png">

I did not know what a shield was at first, but after watching this [tutorial](https://www.youtube.com/watch?v=Dl-ekLb4quE&t=274s) on how to add shields in Github, it was a relatively straightforward assignment.


### Step 1
Look at the architecture in the repository that is required to run the software and any other shields that needs to be added to the README, like license or contributor shields. Proceed to [shields.io](https://shields.io/). 


### Step 2
For the architecture shields, click on "Build". Scroll down the page until you see "Your Badge" followed by three fields labeled as "label", "message", and "color":  
<img width="252" alt="image" src="https://user-images.githubusercontent.com/62410569/200581554-a78dea2f-489b-4fed-8269-ecf2b8c9fa56.png">

For the label field type in "architecture", for the message field type in all the compatible architecture types that was found in the repository, and for the color field choose green. Click on "Make Badge" and the resulting shield should look something like [this](https://img.shields.io/badge/architecture-arm64%2C%20amd64%2C%20arm-green). Copy the URL and go to your fork on Github to paste the URL into the README in the format ![](/*URL*/) and the README should now have the shield icon.

If the issue asks for a contributor shield, go back to shields.io and type in "contributors" in the search/project URL field. Look for Github contributors and click it.
You should be forwarded to a page that looks like this:
<img width="585" alt="image" src="https://user-images.githubusercontent.com/62410569/200589237-3a36a2f3-e6a3-4891-9507-00a3de955394.png">


Select "contributors" in the variant field, type "open-horizon-services" in the user field, type in the repository name for the repo field, and all other fields stay the default. The preview should show the count of contributors in the repository and should change color depending on how many contributors there are. Copy the Badge URL and go back to your fork to paste the URL in the same format as the architecture shield: ![](/*URL*/).

If the issue asks for a license shield, you first check to see if the repository has a license. If so, repeat the same steps for adding the contributor shield, except type in "license" in the search/project URL field instead of "contributors". If the repository has no license, you must add a LICENSE file. Click on "Add file" in the repository 

<img width="81" alt="image" src="https://user-images.githubusercontent.com/62410569/200592386-94d1661c-74c2-4b5d-a7ac-515244358fd1.png">
Then click on "Create new file" and type "LICENSE" as the name of the title and you should recieve the option to choose a license template.
<img width="151" alt="image" src="https://user-images.githubusercontent.com/62410569/200593227-6be4fefa-47d8-40aa-8352-71b83b7db0ff.png">
Click on this option and you will be brought to a page with various licenses for your project. For Open Horizon, choose Apache License 2.0 and then click on Review and submit. Now that the license has been added, add the shield for the license.

### Step 3
After all the shields have been added to your fork, submit and sign off on a pull request to merge into the main open-horizon-services branch.
<img width="924" alt="image" src="https://user-images.githubusercontent.com/62410569/200595310-ede04738-d757-4cce-bd16-8ca2d12a96be.png">
### What I Learned
This assignment has taught me what shields are and how I can add them to my projects. I also learned how to add a License to my project. Because this was among one of my first assignments in Open Horizon and Github, I learned the workflow of these assignments.

## Adding MAINTAINERS.md
This type of issue was labeled "good first issue" and was simple to complete. 
### Step 1
Fork the repository.
### Step 2
Create a new file and call it "MAINTAINERS.md".
### Step 3
In MAINTAINERS.md, create a table and add all the maintainers of the project into the table; add their name, Github username, and email. 
<img width="706" alt="image" src="https://user-images.githubusercontent.com/62410569/200605774-ef7c5115-bb02-48bd-a1c8-689ed217abfc.png">
### Step 4
Submit and sign off on a pull request to merge into the main open-horizon-services branch.
<img width="920" alt="image" src="https://user-images.githubusercontent.com/62410569/200606272-e43eafc6-beeb-47e3-9d2b-105097492c21.png">
### What I Learned
I learned more about formatting in Github and how to make a table.

## Adding Makefile targets and horizon files
This a more difficult assignment and I am currently in the process of figuring out what PHONY targets are, how to create the requested Makefiles, and how to test and verify with an Open Horizon Agent.
### Step 1
Fork the repository and clone the files onto your laptop.
### Step 2
Add the following Makefile targets:

    publish-service:

    publish-pattern:

    register-pattern:
    
and populate the targets with the following code:

<img width="463" alt="image" src="https://user-images.githubusercontent.com/62410569/201499034-06c107b9-167d-4e97-88e8-38cfd62cd279.png">
The newly created targets must also be listed in Phony:
<img width="583" alt="image" src="https://user-images.githubusercontent.com/62410569/201499169-6782e1ba-c795-4abf-86e0-1869701e1d32.png">

### Step 3
We must now install an Open Horizon agent onto our laptop. Unfortunately the Open Horizon scripts use `systemd` to deploy daemon processes but the WSL2 ubuntu image uses `init.d` as PID 1 instead of `systemd`. This prevents the installation of the Open Horizon daemons. To fix this, follow these [instructions](https://github.com/open-horizon/devops/pull/113/files?short_path=d2366d6#diff-d2366d693f6bd1eecc1802726c1181474816e9fafb25e3e98db3f85073150572).

### Step 4
Create a folder and open WSL. Gain read and write access to all files/commands by rooting. To do this, use the command `sudo -i` and input your password for your laptop. After the account has been rooted, cd into the folder that was created. Next, input the following lines of code into the terminal:
```
export HZN_ORG_ID=examples
export HZN_DEVICE_TOKEN= # specify a string value for a token
export HZN_DEVICE_ID= # specify a string value for the node ID
export HZN_EXCHANGE_USER_AUTH=student:RCOS
export HZN_EXCHANGE_URL=http://132.177.125.232:3090/v1
export HZN_FSS_CSSURL=http://132.177.125.232:9443/
export HZN_AGBOT_URL=http://132.177.125.232:3111/
export HZN_SDO_SVC_URL=http://132.177.125.232:9008/api
```
where HZN_DEVICE_TOKEN can be your name and HZN_DEVICE_ID can be your device name. Next, create a file named `agent-install.cfg` inside the folder. Open `agent-install.cfg` and input the urls from the terminal:
```
export HZN_EXCHANGE_URL=http://132.177.125.232:3090/v1
export HZN_FSS_CSSURL=http://132.177.125.232:9443/
export HZN_AGBOT_URL=http://132.177.125.232:3111/
export HZN_SDO_SVC_URL=http://132.177.125.232:9008/api
```
Now as **root** input the following command:

`curl -sSL https://github.com/open-horizon/anax/releases/latest/download/agent-install.sh | bash -s -- -i anax: -k ./agent-install.cfg -c css: -p IBM/pattern-ibm.helloworld -w '*' -T 120`
To see if you have successfully installed the agent, try typing in some commands. If you type in `hzn version` you should recieve something like this:

<img width="492" alt="image" src="https://user-images.githubusercontent.com/62410569/201500236-1c062d5c-6d8a-4fad-99b9-e311ce64a794.png">

If you type in `hzn node list` you should see the fields that you exported and the URLs that are in the configuration file:

<img width="505" alt="image" src="https://user-images.githubusercontent.com/62410569/201500292-57942a62-1e14-44d7-baf4-4f51e43f6375.png">

You can see if Docker is also installed by typing in `docker ps`:

<img width="495" alt="image" src="https://user-images.githubusercontent.com/62410569/201500363-21b21db5-6bdb-4350-926e-635a004ee6ff.png">

`hzn exchange status` will give the status of the hub:

<img width="543" alt="image" src="https://user-images.githubusercontent.com/62410569/201500497-edf1bb12-bfb9-4d3a-8efa-3f1b8b237b9f.png">

`hzn exchange user list` will list information about the user:

<img width="563" alt="image" src="https://user-images.githubusercontent.com/62410569/201500503-5067f598-75dd-4000-8823-337f110db9c9.png">

> There is an issue with the Dockerfile. When performing a Docker build with `make dev`, it gives an [error](https://github.com/open-horizon-services/web-helloworld-c/issues/12).

> //work in progress
