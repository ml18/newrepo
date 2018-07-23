# newrepo 

This is sample AWS Jupyter Notebook Server Setup Steps:

* Step 1 (ssh key): In Local Linux, using "ls ~/.ssh" to make sure there is no ssh key already, then use "ssh-keygen" to generate ssh key: id_rsa and id_rsa.pub ->copy the id_rsa.pub to desktop so we can easily copy it
* Step 2 (AWS EC2 Key pair): AWS EC2 -> NetWork & Security->Key Pair->Import Key Pair->Choose From File-> select the id_rsa.pub above on desktop->Click "Import"
* Step 3 (AWS EC2 security group): AWS EC2 -> NetWork & Security->Security Groups-> create UCLA DS security group (ssh/port 22/Anywhere, http/port 80/Anywhere, https/port 443/Anywhere, PostgreSQL/5432/Anywhere, Custom TCP/port 27016/Anywhere)
* Step 4 (AWS EC2 Instance): AWS EC2 Instance->select Linux server image "Ubuntu Server 16.04 LTS"->t2.micro (CPU=1, Mem=1)-> add storage: 20GB for EBS->security group: choose the above created security group UCLA DS security group->review->launch using existing key pair created above->view instance: Ppv4 public IP: 54.85.184.98 (as example for the following illustration)
* Step 5,6,7 (docker): Go to Local Linux-> run "ssh ubuntu@54.85.184.98" to log into AWS EC2 created above ->run "curl -sSL https://get.docker.com | sh" to get docker image in EC2 instance->run "sudo usermod -aG docker ubuntu" to change the docker security -> run "exit" to exit sytem to make the docker security to take effect -> re-log into EC2 instance by running "ssh ubuntu@54.85.184.98"-> run "docker -v" to chec docker version->run "docker pull ubuntu"-> run "docker run -t ubuntu bash"  to make docker running on EC2 instance-> run "docker images" to check docker images on system-> run "docker ps -a" to make sure docker ubuntu is running on EC2 instance (later on if we no longer need them , run "docker system prune" to get rid of them)
* Step 8 (Jupyter NoteBook): on the above docker container -> run "docker pull jupyter/datascience-notebook"-> run the following to get juyper notebook up running 
"docker run \
 -d \
 -p 443:8888 \
 -v /home/ubuntu:/home/joyyan \
 jupyter/datascience-notebook" (we can also put these to .profile as alias j=... for later easy use)-> run "docker ps -a" to get juyper's id (6c43xxxx), port, name...->run "docker logs 6c43" or "docker exec 6c43 jupyter notebook list" to get the jupyter token used in the next step
* Step 9 (Get Jupyter up and running to write Python or R code): on web URL type in above EC2 public Ip address 54.85.184.98:443-> enter jupyter token given in above step 6's last piece-> Jupyter Notebook pop up on the screen->start to write Python or R code in it
* note: we can use "tmux" to make the connection more stablized if desired (if so, starting it from above step 5 after get into EC2 instance)
* a diagram of the system briefly illustrated as the following:
<image src="AWS_system_diagram.jpeg" width=300>
