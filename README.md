# Deploying a Node Js Application on AWS EC2

### Testing the project locally

1. Clone this project
```
git clone https://github.com/jocasantos/aws-nodejs-app-demo.git
```
2. Setup the following environment variables - `(.env)` file
```
DOMAIN="http://localhost:3000"
PORT=3000
STATIC_DIR="./client"
```
3. Initialise and start the project
```
npm install
npm run start
```

### Set up an AWS EC2 instance

1. Create an IAM user & login to your AWS Console
    - Access Type - Password
    - Permissions - Admin
2. Create an EC2 instance
    - Select an OS image - Ubuntu
    - Create a new key pair & download `.pem` file
    - Instance type - t2.micro
3. Connecting to the instance using ssh
    - First make the .pem file only readable for you (security measure)
    - Come back to CLI and go to .pem file directory
```
chmod 400 <FILENAME>.pem
```
   - Now connect to EC2 instance using SSH
```
ssh -i instance.pem ubunutu@<IP_ADDRESS>
```

### Configuring Ubuntu on remote VM

1. Updating the outdated packages and dependencies
```
sudo apt update
```
3. Install Git - [Guide by DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-git-on-ubuntu-22-04) 
4. Configure Node.js and `npm` - [Guide by DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-22-04)

### Deploying the project on AWS

1. Clone this project in the remote VM
```
git clone https://github.com/jocasantos/aws-nodejs-app-demo.git
```
2. Go to aws-nodejs-app-demo directory
```
cd aws-nodejs-app-demo
```
3. Create the .env file
```
vim .env
```
4. Setup the following environment variables - `(.env)` file
```
DOMAIN="http://localhost:3000"
PORT=3000
STATIC_DIR="./client"
```
> To acess our EC2 instance from the Internet we have to acess the Public IPv4 adress's instance (eg. 22.333.22.22)

5. Initialise and start the project
```
npm install
npm run start
```

> NOTE - We will have to edit the **inbound rules** in the security group of our EC2, in order to allow traffic from our particular port (eg. 3000)

6. Edit the **inbound rules**
   - Select our instance on the instances dashboard and go to "Security" tab
   - Open "Security groups" link
   - Go to "Edit inbound rules"
   - Add rule, Port range: 3000, Ip ranges: 0.0.0.0/0 (this means from anywhere), and leaves everything else default.
  
> Go to your browser and connect to your instance, Public IPv4 adress + Port (eg. 22.333.22.22:3000)!

### Project is deployed on AWS 🎉
