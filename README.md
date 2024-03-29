# Using Terraform Provisioners to Set Up an Apache Web Server on AWS

Clone the required code from the provided repository:

1. `git clone https://github.com/linuxacademy/content-hashicorp-certified-terraform-associate-foundations.git`
Switch to the directory where the code is located:

2. `cd content-hashicorp-certified-terraform-associate-foundations/section3-hol2/`
List the files in the directory:

`ls`
The files in the directory should include main.tf, README.md, and setup.tf.

Examine the Code in the main.tf File
View the contents of the main.tf file using the cat command:

`cat main.tf`
Examine the code in the resource block and note the following:

3. We are creating an AWS EC2 instance (virtual machine) named webserver.

We are passing a number of parameters for the resource, such as the AMI that the VM will be spun up as, the instance type, the private key that the instance will be using, the public IP attached to the instance, the security group applied to the instance, and the subnet ID where the VM will be spun up.

Note: All of these resources are actually being created via the setup.tf file, which you can view if desired.

4. Examine the code in the provisioner block and note the following:

The remote-exec keyword tells us that this is a remote provisioner, which invokes a script on a remote resource after it is created.
The provisioner is using the parameters configured in the embedded connection block to connect to the AWS EC2 instance being created.
The provisioner will then issue the commands configured in the inline block to install Apache webserver on CentOS through the yum package manager, start up the Apache server, create a single web page called My Test Website With Help From Terraform Provisioner as an index.html file, and move that file into the data directory of the webserver to be served out globally.
Deploy the Code and Access the Bootstrapped Webserver
Initialize the Terraform working directory, and download the required providers:

`terraform init`
Validate the code to look for any errors in syntax, parameters, or attributes within Terraform resources that may prevent it from deploying correctly:

`terraform validate`
You should receive a notification that the configuration is valid.

Review the actions that will be performed when you deploy the Terraform code:

`terraform plan`
In this case, it will create 7 resources as configured in the Terraform code.

Deploy the code:

`terraform apply`
When prompted, type yes, and press Enter.

As the code is being deployed, you will notice that the Terraform provisioner tries to connect to the EC2 instance, and once that connection is established, it will run the bootstrapping that was configured in the provisioner block against the instance.

When complete, it will output the public IP for the Apache webserver as the Webserver-Public-IP value.

Copy the IP address, paste it in a new browser window or tab, and press Enter.

Verify that the web page displays as My Test Website With Help From Terraform Provisioner, validating that the provisioner within your code worked as intended. The commands configured in the provisioner code were issued and executed successfully on the EC2 instance that was created.
