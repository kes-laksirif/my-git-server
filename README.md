# my-git-server
## How to Setup a Git Server

#### Setup Server

##### install git
```
sudo apt update && sudo apt install git
```

##### Create a new user named git
```
sudo useradd -r -m -U -d /home/git -s /bin/bash git
```

##### Switch to git user su
```
sudo su - git
```

##### To create the SSH directory and set the correct permissions
```
mkdir -p ~/.ssh && chmod 0700 ~/.ssh
```

##### Create a file named ~/.ssh/authorized_keys which will hold the authorized users’ SSH keys
```
touch ~/.ssh/authorized_keys && chmod 0600 ~/.ssh/authorized_keys
```

##### Initiate a new empty repository in server
```
git init --bare ~/projectname.git
```

#### Setup Local Machine

##### Check if SSH keypair exists
```
cat ~/.ssh/id_rsa.pub
```

##### If not create one using
```
ssh-keygen -t rsa -b 4096 -C "keslaksiri@gmail.com"
```
Copy key using above cat command

##### Add key in server
Copy the output from the cat command above and go back to the Git server console.

On the server, open your text editor and paste the public key that you copied from your local machine into the ~/.ssh/authorized_keys file

##### Check if key added 
```
sudo nano /home/git/.ssh/authorized_keys
```

#### Connect local git to server

##### Create
```
cd /path/to/local/project
git init
git remote add origin git@git_server_ip:projectname.git
touch test_file
git add .
git commit -m "descriptive message"
git push -u origin master
```

##### To change password of git user
```
sudo passwd git
```

##### If cannot connect using SSH - remove and add again ssh
```
sudo apt-get remove openssh-client openssh-server
sudo apt-get install openssh-client openssh-server
```



##### To save and exit in vi editor
```
press esc key
:wq
press enter
```





https://linuxize.com/post/how-to-setup-a-git-server/
