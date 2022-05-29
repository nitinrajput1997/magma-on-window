# magma-on-window

### Install WSL

### Open wsl terminal

### Install Ansible
```bash
sudo apt remove ansible
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible -y
```
### Copy your public SSH key to the host:
```bash
ssh-keygen -R 192.168.5.92
ssh-copy-id ubuntu@192.168.5.92
```
### Clone code
```
git clone https://github.com/ShubhamTatvamasi/magma-galaxy.git
```
### Update your host value in hosts.yml file

### Deploy Magma orchestrator:
```bash
ansible-playbook deploy-orc8r.yml
```
### Create a user 
```bash
ssh ubuntu@192.168.5.92

ORC_POD=$(kubectl -n orc8r get pod -l app.kubernetes.io/component=orchestrator -o jsonpath='{.items[0].metadata.name}')
kubectl -n orc8r exec -it ${ORC_POD} -- envdir /var/opt/magma/envdir /var/opt/magma/bin/accessc \
  add-existing -admin -cert /var/opt/magma/certs/admin_operator.pem admin_operator

NMS_POD=$(kubectl -n orc8r get pod -l app.kubernetes.io/component=magmalte -o jsonpath='{.items[0].metadata.name}')
kubectl -n orc8r exec -it ${NMS_POD} -- yarn setAdminPassword magma-test admin admin
kubectl -n orc8r exec -it ${NMS_POD} -- yarn setAdminPassword master admin admin
```
### Access Magma Dashboard

Paste the generated dns (which comes when ansible script completes all tasks successfully) to the location **C:\Windows\System32\drivers\etc\hosts**
