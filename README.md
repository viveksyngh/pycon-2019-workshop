# OpenFaaS Workshop

## Prerequisite:
1. [Github Account](https://www.github.com)
2. [DockerHub Account](https://www.dockerhub.com)
3. [Digital Ocean](https://www.digitalocean.com)
(It is recommended to complete this workshop using Digital Ocean)
> Note: If you already have a DigitalOcean account it's great. If you don't, you can create using [this](https://m.do.co/c/1edc3a68b25d) referral link which will give you $50 free credit. You may need to put your credit card details which you can remove later. 

# Important Links:

1. Workshop VSCode Tool (https://github.com/openfaas-incubator/workshop-vscode)
2. Workshop lab resources (https://github.com/openfaas/workshop)
3. OpenFaas Documentation (https://docs.openfaas.com/)

You can either use Local Desktop with Docker installed or a VM provisioned on any cloud platform (preferably Digital Ocean) with a script created by community to automate OpenFaaS installation.


## Install and Setup Digital Ocean CLI(`doctl`)

### Install `doctl` 

To install `doctl` suitable for your operating system, please follow the instructions listed on the below page under installation section.

[Install `doctl` cli](https://github.com/digitalocean/doctl/blob/master/README.md#installing-doctl)

### Get access token for CLI
In order to use doctl, you need to authenticate with DigitalOcean by providing an access token, which can be created from the [Applications & API](https://cloud.digitalocean.com/settings/api/tokens) section of the Control Panel. 

[Generate access token](https://www.digitalocean.com/docs/api/create-personal-access-token/)

### Authenticate your CLI using DigitalOcean 

After generating access token, you need to authenticate the `doctl` cli with Digital Ocean using access token generated in previous step. Follow the instructions at below link to authenticate.

[Authenticating with DigitalOcean](https://github.com/digitalocean/doctl/blob/master/README.md#authenticating-with-digitalocean)

## Setting up environment using K3S and VSCode on Digital Ocean
This option uses k3s which lightweight kubernetes distribution from rancher labs and VScode in browser running on remote server

### If Digital Ocean client (`DOCTL`) is installed.

#### Clone the repository and run the provision script

Clone the repository on you local system and run provision script

```
git clone https://github.com/openfaas-incubator/workshop-vscode && cd workshop-vscode
```
```
./provision-digitalocean.sh
```

> Note: By default, the region in which your VM is created will be London. You can edit that in `provision-digitalocean.sh` script and update it to `BLR1` for bangalore. `REGION="blr1"`

### If Digital Ocean client (`DOCTL`) is not installed.

#### Create Droplet 
If you don't have `doctl` (Digital Ocean CLI) installed and setup, Please go ahead and create a droplet with below specification using 
Digital Ocean UI.

1. SIZE="s-2vcpu-4gb"
2. IMAGE="ubuntu-16-04-x64"
3. REGION="blr1"

Once droplet is created, you will receive one time password on your email. SSH to the machine using root user and Public IP. It will also ask you to change the password, please change the password and remember it. 

#### Setup the environment
Clone the `workshop-vscode` repository and run the setup script inside the droplet
```
git clone https://github.com/openfaas-incubator/workshop-vscode && cd workshop-vscode
```
```
bash cloudinit.txt
```



### Find password for VSCode browser login
ssh to digital ocean droplet and run below command to get password to login into VSCode browser 

```
docker logs vscode | grep -i password
```

> It takes time to download the images and run it. Please wait for sometime to get it downloaded and then run the command. To validate whether container is running or not run `docker ps`, you should see container with name `vscode`.

Find this password and save it, you may need this later

### Login into VScode
Go to browser and open `https://<droplet-public-ip>:8443`, you will prompted for the password. Enter the password retrieved in previous step and login. 

> You will need to accept the self-signed certificate, which will display as "insecure". Despite the warning, it will provide encryption for your connection.

Once you login to the VSCode, there are some steps that you need to follow and instructions are present inside openfaas folder.

Open a terminal window in vscode

1. Add `export OPENFAAS_URL=<droplet-public-ip>:31112` to .bashrc (`01-add-to-bashrc.txt`). 
2. Login to the gateway using `faas-cli` command present in file `02-run-this.txt`
3. Type Gateway URL from file `03-gateway-url.txt` in browser and login using the gateway password listed in `04-gateway-password.txt` file.


## Starting the workshop

> If you are running the workshop on your local machine, you will have start from the workshop Lab 1. For the workshop on Digital Ocean with VSCode, you can skip the Lab 1 and start from Lab 2.

> Some place you might see URL and instruction which assumes you are working on local host. In that case you may need to replace 127.0.0.1 with your public IPs. 

> faas-cli and faas are same, faas is an alias of faas-cli

> OpenFaaS comes with UI and CLI to interact with OpenFaaS. UI is can be used list function and test them. CLI is more powerful than UI and it has lot of functionality.


# [Lab 2](https://github.com/openfaas/workshop/blob/master/lab2.md)


This lab familiarize you with OpenFaaS UI, CLI and how to manage functions using them. Also, you will be deploying Grafana dashboard to monitor functions metrics.

> Note: In CLI section, export instructions can be skipped but you can read through them.

# [Lab 3](https://github.com/openfaas/workshop/blob/master/lab3.md) 

> Login to your docker hub account using below command in the terminal before working on this lab
```
docker login
```

We will skip following section from this lab. 
1. Custom templates
2. Custom templates store
3. Variable Substitution in YAML File
4. Custom binaries as functions

# [Lab 4](https://github.com/openfaas/workshop/blob/master/lab4.md) 

This lab goes deeper into functions and covers following
1. Using environment variable
2. Using HTTP Context like query string, path, headers
3. Read only file systems
4. Logging
5. Chaining Functions

# [Lab 5](https://github.com/openfaas/workshop/blob/master/lab5.md) 
In this lab we will create Github Bot. 

If you are running the workshop on digital ocean then you can skip set up a tunnel with ngrok and log into the gateway with the ngrok address section.

# [Lab 6](https://github.com/openfaas/workshop/blob/master/lab6.md)

This lab covers, how you can renders HTML using your functions and create single page applications (SPA).

# [Lab 7](https://github.com/openfaas/workshop/blob/master/lab7.md)
This lab covers following
1. Difference between synchronous callbacks and asynchronous callbacks.
2. Using `X-Callback-Url` header
