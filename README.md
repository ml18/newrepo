# newrepo 

This is sample AWS Jupyter Notebook Server Setup Steps:

* In Linux, using "ls ~/.ssh" to make sure there is no ssh key already, then use "ssh-keygen" to generate ssh key: id_rsa and id_rsa.pub
* copy the id_rsa.pub to desktop so we can easily copy it
* AWS EC2 -> NetWork & Security->Key Pair->Import Key Pair->Choose From File-> select the id_rsa.pub above on desktop->Click "Import"
* AWS EC2 -> NetWork & Security->Security Groups-> create UCLA DS security group (ssh/port 22/Anywhere, http/port 80/Anywhere, https/port 443/Anywhere, PostgreSQL/5432/Anywhere, Custom TCP/port 27016/Anywhere)
