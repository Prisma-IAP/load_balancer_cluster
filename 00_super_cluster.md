# LOAD BALANCER STARTER

--Single-board Computer Super Cluster

In this tutorial I'm following all steps from **NetworkChuck** YouTube's Channel.

[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/X9fSMGkjtug/0.jpg)](http://www.youtube.com/watch?v=X9fSMGkjtug)

# CONFIGURAÇÕES INICIAIS RASPBERRY E ORANGE

## Step 1 - Installing Your Operating System:
- On Orange Pi you can install Ubuntu Server (available on Orange Pi official website)
- On Raspberry Pi you can install Raspberry Pi OS Lite (available on Raspberry Pi Imager)
  - Open `/boot/cmdline.txt` file and add this information (`cgroup_memory=1 cgroup_enable=memory ip=ip_address::default_gateway:subnet_mask:your_hostname:eth0:off`) at the end of the line
  - Open `/boot/config.txt`file and add this information (`arm_64bit=1`) at the end of the file
  - Create a new blank file `ssh` on boot folder
  - Login on your server node and enter as *sudo user* with `sudo su -` command
  - Run the command `sudo iptables -F` and reboot your machine

## Step 2 - K3S Installation on Master node:
- Run the command `curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" sh -s -` for K3S installation
- Get K3S token by running this command: `cat /var/lib/rancher/k3s/server/node-token`

## Step 3 - K3S Installation on Worker node:
- Run the command `curl -sfL https://get.k3s.io | K3S_URL=https://server_ip:6443 K3S_TOKEN="server_token" K3S_NODE_NAME="chosen_node_name" sh -` on all nodes for installation


## Step 4 - (Optional) Rancher Installation:
(FERRAMENTA DE MONITORAMENTE EM INTERFACE)
- First you need another virtual machine different of your master and worker machines
- I believe Open Lens is another good option for a dashboard

## Step 5 - Create your deployment file:
- Create your deployment.yaml file
- Apply your configuration running the command: `kubectl apply -f deployment.yaml`

## Step 6 - Create your deployment file:
- Create your service.yaml file
- Apply your configuration running the command: `kubectl apply -f service.yaml`

## Step 7 - Load Balancing:
- Create another deployment.yaml and service.yaml files or just create a single file with all settings
- Apply all settings by running `kubectl apply -f` command

## Step 8 - Ingress:
- Create your ingress.yaml file
- On Windows machine, edit **hosts** file on path `C:\Windows\System32\drivers\etc` and in a new line add an ip address followed by your custom host name, eg: `192.168.0.11 afarmwithcows.com`
- Access **afarmwithcows.com** on your browser

## Step 9 - Scaling Up/Down
- For up/down pod scaling, just run the following command with a chosen number: ``kubectl scale deployment/rancher-app --replicas=15``
