#**Intel Developer Cloud - Guidelines**
# **Intel Developer Cloud - Guidelines**

One can follow the procedure to the setup the IDC - **https://youtu.be/PhzlMQ8-GE4**
![SSetting](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/aadfb1c7-7ba3-494e-b7db-5dd236446522)

Step by Step Guidelines for setting up the IDC and to launch the Jupyter Notebook.
# One can follow the procedure to the setup the IDC -  <a href="https://youtu.be/PhzlMQ8-GE4"><img src="https://github.com/shriramkv/SYCLwithIDC/assets/72274851/693730f3-cda3-4a02-9c63-5b3ac1838ad7" height="70" width="70"></a>

1.	Generate an ssh key using the command ssh-keygen in the power shell as an administrator. 
## Step by Step Guidelines for setting up the IDC and to launch the Jupyter Notebook.

2.	Open the generated key file using notepad and copy the contents of the file.(C:\Users\<<username>>\.ssh is the path - file name is id_rsa.pub, use the command notepad id_rsa.pub) 
### 1.	Generate an ssh key using the command ssh-keygen in the power shell as an administrator. 

3.	Nextly login or register into the Developer Cloud and add the key under the profile section. https://scheduler.cloud.intel.com/
### 2.	Open the generated key file using notepad and copy the contents of the file.(C:\Users\<<username>>\.ssh is the path - file name is id_rsa.pub, use the command notepad id_rsa.pub) 

4.	Open .ssh folder and create a config file with the below commands:
Host myidc
Hostname idcbetabatch.eglb.intel.com
User uXXXXXX #← Request "scheduled access" at https://scheduler.cloud.intel.com/#/systems" to get your user identifier.
IdentityFile ~/.ssh/id_rsa
#ProxyCommand ncat --proxy YourProxy:XXXX %h %p --proxy-type socks5 %h %p  ## Uncomment if necessary
ServerAliveInterval 60
ServerAliveCountMax 10
StrictHostKeyChecking no 
UserKnownHostsFile=/dev/null
![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/4f51e91c-be8a-461b-8292-38b147f0c342)<br>
![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/f049dd0d-c001-48d2-9cad-3623b723c98f)<br>

5.	On Powershell type ssh myidc to connect to your head node instance. This will enable you to be authenticated. 
### 3.	Nextly login or register into the Developer Cloud and add the key under the profile section. https://scheduler.cloud.intel.com/

6.	Next to connect to an interactive node type in the below command:
srun --pty bash
source /opt/intel/oneapi/setvars.sh
This will get the batch node activated! You will see this clearly in the powershell terminal. u***@idc-beta-batch-head-node would get changed to u***@idc-beta-batch-pvc-node
7.	Configure your shell using the command conda init bash
![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/0639e4d6-ef69-4370-bae8-f3f38503d7b9)<br>

8.	Close the existing instance to make sure that the configuration changes reflect using the command exit
9.	You are taken back to the head node again, connect to the interactive node again by repeating Step6 again.
### 4.	Open .ssh folder and create a config file with the below commands:
Host myidc <br>
Hostname idcbetabatch.eglb.intel.com <br>
User uXXXXXX #← Request "scheduled access" at https://scheduler.cloud.intel.com/#/systems" to get your user identifier. <br>
IdentityFile ~/.ssh/id_rsa <br>
#ProxyCommand ncat --proxy YourProxy:XXXX %h %p --proxy-type socks5 %h %p  ## Uncomment if necessary <br>
ServerAliveInterval 60 <br>
ServerAliveCountMax 10 <br>
StrictHostKeyChecking no <br>
UserKnownHostsFile=/dev/null <br>

10.	To check the available environments type in the command conda env list
### 5.	On Powershell type `ssh myidc` to connect to your head node instance. This will enable you to be authenticated. 

11.	Choose the environment of your choice by typing in conda activate env_name
### 6.	Next to connect to an interactive node type in the below command:
`srun --pty bash` <br>
`source /opt/intel/oneapi/setvars.sh` <br>

12.	Get and check the allocated socket by using the below command:
echo $(ip a | grep -v -e "127.0.0.1" -e "inet6" | grep "inet" | awk {'print($2)}' | sed 's/\/.*//')
#### This will get the batch node activated! You will see this clearly in the powershell terminal. u***@idc-beta-batch-head-node would get changed to u***@idc-beta-batch-pvc-node

13.	Note down the last 2 digits of the ip address.

14.	To activate Jupyter Lab use the following command:
jupyter-lab --ip 10.10.10.X  (Where X is the last two digits that you observed before in Step13)
### 7.	Configure your shell using the command conda init bash

15.	Open a fresh Powershell Instance and type ssh myidc -L 8888:10.10.10.X:8888 (Where X is the last two digits that you observed before in Step13)
![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/48ab5585-517a-4d54-a012-51fbaf877fa2)
<br>

16.	Open a local browser and type the following in the address bar: http://localhost:8888/lab
### 8.	Close the existing instance to make sure that the configuration changes reflect using the command exit

17.	In the preceding screen you will be asked for a token. This can be found in the first powershell instance on the 6th last line.
18.	Once done, clone this directory! That's it you can learn SYCL !! The command to do the same is - **git clone https://github.com/shriramkv/SYCLwithIDC**
19.	The above command has to be issued fromt the Jupyter Notebook. 
### 9.	You are taken back to the head node again, connect to the interactive node again by repeating Step6 again.

### 10.	To check the available environments type in the command conda env list

![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/41f9f009-743b-4c06-9807-1932c6b7b843)<br>


### 11.	Choose the environment of your choice by typing in conda activate env_name

### 12.	Get and check the allocated socket by using the below command:

`echo $(ip a | grep -v -e "127.0.0.1" -e "inet6" | grep "inet" | awk {'print($2)}' | sed 's/\/.*//')
`
![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/15b14a38-bf68-433a-91e2-1b21388e2081)
<br>

### 13.	Note down the last 2 digits of the ip address.

### 14.	To activate Jupyter Lab use the following command:
`jupyter-lab --ip 10.10.10.X  (Where X is the last two digits that you observed before in Step13)
`
![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/eb8e29e5-1ded-4682-9887-3d8acd9dea9f)
<br>

### 15.	Open a fresh Powershell Instance and type ssh myidc -L 8888:10.10.10.X:8888 (Where X is the last two digits that you observed before in Step13)

![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/58526019-dcdf-4834-9460-2c8ad5a5ab49)
<br>

### 16.	Open a local browser and type the following in the address bar: http://localhost:8888/lab

![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/6b16edd6-3414-4d55-aa25-bfac6f800301)
<br>

### 17.	In the preceding screen you will be asked for a token. This can be found in the first powershell instance on the 6th last line.


### 18.	Once done, clone this directory! That's it you can learn SYCL !! The command to do the same is - **git clone https://github.com/shriramkv/SYCLwithIDC**
### 19.	The above command has to be issued fromt the Jupyter Notebook. 


# Where to start SYCL? 
