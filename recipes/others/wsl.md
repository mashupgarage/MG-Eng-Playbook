# Windows Subsystem for Linux (WSL) Setup running Ubuntu

## Basics
This setup will be running on Windows 10 or 11.


## Steps
### WSL installation
Open up PowerShell or Command Prompt (running on administrator)
On the command prompt:
```
wsl install
```
Reboot your PC after a successful installation

To verify installation version, use the command:
```
wsl -l -v
```
The results of said command should point to a version of 2

### Installing Linux distributions

To see a list of available distros:
```
wsl --list --online
```
|NAME         |FRIENDLY NAME      |
|-------------|-------------------|
|Ubuntu       |Ubuntu             |
|Debian       |Debian GNU/Linux   |
|Kali-linux   |Kali Linux Rolling |
|Ubuntu-18.04 |Ubuntu 18.04 LTS   |
|Ubuntu-20.04 |Ubuntu 20.04 LTS   |
|Ubuntu-22.04 |Ubuntu 22.04 LTS   |
|Ubuntu-24.04 |Ubuntu 24.04 LTS   |


From the list select the **name** of the linux distro desired, in this case we are opting for **Ubuntu**
```
wsl --install -d Ubuntu
```

### Installing Docker
Open up PowerShell or Command Prompt and key in **wsl**
On the same terminal, run the following to install all required libraries
```sh
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

Install the docker packages:
```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

To test if docker installed properly:
```sh
sudo docker run hello-world
```

