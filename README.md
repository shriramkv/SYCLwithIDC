# **Intel Developer Cloud - Guidelines**

![SSetting](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/aadfb1c7-7ba3-494e-b7db-5dd236446522)

# Step by Step Guidelines for setting up the IDC and to launch the Jupyter Notebook.<br>
# One can follow the procedure to the setup the IDC - <a href="https://youtu.be/PhzlMQ8-GE4"><img src="https://github.com/shriramkv/SYCLwithIDC/assets/72274851/693730f3-cda3-4a02-9c63-5b3ac1838ad7" height="70" width="70"></a>

### 1.	Generate an ssh key using the command ssh-keygen in the power shell as an administrator. 

### 2.	Open the generated key file using notepad and copy the contents of the file.(C:\Users\<<username>>\.ssh is the path - file name is id_rsa.pub, use the command notepad id_rsa.pub) 

![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/4f51e91c-be8a-461b-8292-38b147f0c342)<br>
![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/f049dd0d-c001-48d2-9cad-3623b723c98f)<br>


### 3.	Nextly login or register into the Developer Cloud and add the key under the profile section. https://scheduler.cloud.intel.com/

![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/dd2308d9-5be6-4de4-82f6-e202741ad62b)


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

### 5.	On Powershell type `ssh myidc` to connect to your head node instance. This will enable you to be authenticated. 

### 6.	Next to connect to an interactive node type in the below command:
`srun --pty bash` <br>
`source /opt/intel/oneapi/setvars.sh` <br>

![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/8d834f65-5a6d-4f96-8d3f-660f8f664097)
![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/e3346e85-8ef6-4c54-a1f4-a500374c8c24)


This will get the batch node activated! You will see this clearly in the powershell terminal. u***@idc-beta-batch-head-node would get changed to u***@idc-beta-batch-pvc-node
### 7.	Configure your shell using the command conda init bash

![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/0639e4d6-ef69-4370-bae8-f3f38503d7b9)<br>

### 8.	Close the existing instance to make sure that the configuration changes reflect using the command exit

#### This will get the batch node activated! You will see this clearly in the powershell terminal. u***@idc-beta-batch-head-node would get changed to u***@idc-beta-batch-pvc-node

### 9.	You are taken back to the head node again, connect to the interactive node again by repeating Step6 again.

### 10.	To check the available environments type in the command conda env list

![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/41f9f009-743b-4c06-9807-1932c6b7b843)<br>


### 11.	Choose the environment of your choice by typing in conda activate env_name

### 12.	Get and check the allocated socket by using the below command:

`echo $(ip a | grep -v -e "127.0.0.1" -e "inet6" | grep "inet" | awk {'print($2)}' | sed 's/\/.*//')
`
<br>
<br>
![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/15b14a38-bf68-433a-91e2-1b21388e2081)
<br>

### 13.	Note down the last 2 digits of the ip address.

### 14.	To activate Jupyter Lab use the following command:
`jupyter-lab --ip 10.10.10.X  (Where X is the last two digits that you observed before in Step13)
`
<br>
<br>
![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/eb8e29e5-1ded-4682-9887-3d8acd9dea9f)
<br>

### 15.	Open a fresh Powershell Instance and type ssh myidc -L 8888:10.10.10.X:8888 (Where X is the last two digits that you observed before in Step13)

![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/58526019-dcdf-4834-9460-2c8ad5a5ab49)
<br>

### 16.	Open a local browser and type the following in the address bar: http://localhost:8888/lab

![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/6b16edd6-3414-4d55-aa25-bfac6f800301)
<br>

### 17.	In the preceding screen you will be asked for a token. This can be found in the first powershell instance on the 6th last line.

<img src="https://github.com/shriramkv/SYCLwithIDC/assets/72274851/95d01c65-770d-4fbc-a528-3c241b3a4b45" width="650px" height="450px">

### 18.	Once done, clone this directory! That's it you can learn SYCL !! The command to do the same is - ![image](https://github.com/shriramkv/SYCLwithIDC/assets/72274851/209bae3e-e0f9-4084-8860-c213b1b53302)

**`git clone https://github.com/shriramkv/SYCLwithIDC`**
### 19.	The above command has to be issued from the Jupyter Notebook. 


# Where to start SYCL? <img src="https://github.com/shriramkv/SYCLwithIDC/assets/72274851/d922b9f5-8b1e-4052-a99c-7d462f36c05b" height="50" width="50">

<a href="https://jupyter.oneapi.devcloud.intel.com/user/u184713/lab/tree/oneAPI_Essentials/"><img src="https://github.com/shriramkv/SYCLwithIDC/assets/72274851/7cb7b880-9f4e-40bf-8792-7745b38c1fb0" height="90" width="90"></a>

**Link:- https://jupyter.oneapi.devcloud.intel.com/user/u184713/lab/tree/oneAPI_Essentials/
**
