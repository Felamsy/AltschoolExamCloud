EXAMINATION PROJECT

### DIGITAL OCEAN DROPLET(vagrant machINE)

### REQUIREMENT

CREATE IAM USER & ACCESS KEYS (Store access key for use)
INSTALL TERRAFORM
INSTALL KUBECTL
INSTALL HELM

### CREATING AN IAM USER ON AWS

1. Log in to the AWS Management Console.
2. Go to the IAM service.
3. Click on the "Users" section on the left-side panel.
4. Click on the "Add user" button.
5. Enter a name for the user.
6. Choose the necessary permissions for the user.
7. Click on the "Next: Review" button
8. Review the user details and click on the "Create user" button.
9. Save the Access key ID and Secret access key for the user.

### ADDING ACCESS AND SECRET ACCESS KEY TO AWS CLI

In this section we are going to be adding the access key and secret access key to the AWS CLI

1. Open the terminal or command prompt

2. Login to your linux server

3. Run this command below

sudo apt update && sudo apt dist-upgrade -y

sudo apt install awscli

4. After running these commands in your terminal you can run the AWS CLI to be sure that it is installed.

5. Configuring Our Aws Cli
   Type "aws configure" and press enter.

Enter the Access key ID and press enter.

Enter the Secret access key and press enter.

Enter the Secret access key and press enter.

Choose the default region name or enter a custom one.

Choose the default output format or enter a custom one(JSON Recommended)

The Access key ID and Secret access key are now set up in AWS CLI and you can use them to run AWS commands.

### INSTALLING TERRAFORM

To install terraform you visit this site: https://developer.hashicorp.com/terraform/downloads

You can see in the operating system the different types you can install on. we are going with Linux and Ubuntu/Debian.

1. wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg

2. $ echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

3. $ sudo apt update && sudo apt install terraform

above are the commands you will copy one by one and run on your ubuntu machine.

terraform -v

the above is the command to check if terraform is installed

### INSTALLING KUBECTL

1. Download the latest kubectl binary from the Kubernetes release page using curl command:
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
   This will download the kubectl binary for the latest stable release.
2. Verify the downloaded binary with SHA-256 checksum using the following command:
   echo "$(<kubectl.sha256) kubectl" | sha256sum --check
   This will verify the downloaded binary with the SHA-256 checksum from the Kubernetes release page
3. Install the kubectl binary by copying it to the appropriate directory:
   sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
   This will install the kubectl binary to the /usr/local/bin directory, which is usually included in the system's PATH environment variable.
4. Verify the installation by running the kubectl version command:
   kubectl version
   This should output the Client Version and Server Version of kubectl.

That's it! You should now have kubectl installed on your Linux system.

### INSTALLING HELM

1. Download the appropriate Helm binary from the Helm release page using curl command:
   curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
   This will download the Helm binary script and execute it to install Helm
2. Verify the installation by running the helm version command:
   helm version
   This should output the Client Version and Server Version of Helm.

That's it! You should now have Helm installed on your Linux system.

Note: If you want to use Helm to deploy applications to a Kubernetes cluster, you also need to configure Helm to work with the cluster. This involves initializing Helm on the cluster, and configuring Helm to use the appropriate Kubernetes context. Here are the general steps to do this:
I) Initialize Helm on the cluster by running the helm init command:
This will install the Tiller server-side component of Helm on the cluster.
II) Create a Kubernetes service account and cluster role binding for Tiller:
kubectl create serviceaccount tiller -n kube-system
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
kubectl patch deploy tiller-deploy -n kube-system --type=json --patch='[{"op": "add", "path": "/spec/template/spec/containers/0/command", "value": ["/tiller", "--listen=localhost:44134"]}]'
III)Configure Helm to use the Kubernetes context for the cluster by running the helm init command with the --service-account and --history-max flags:
helm init --service-account tiller --history-max 200
This will configure Helm to use the tiller service account and set the maximum number of revisions to keep in the release history to 200.

That's it! You should now be able to use Helm to deploy applications to your Kubernetes cluster.

