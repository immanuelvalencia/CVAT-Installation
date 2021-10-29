# CVAT Installation for Ubuntu 20.04




## Ubuntu 18.04 (x86_64/amd64)[](https://openvinotoolkit.github.io/cvat/docs/administration/basics/installation/#ubuntu-1804-x86_64amd64)

-   Open a terminal window. If you don’t know how to open a terminal window on Ubuntu please read  [the answer](https://askubuntu.com/questions/183775/how-do-i-open-a-terminal).
    
-   Type commands below into the terminal window to install  `docker`. More instructions can be found  [here](https://docs.docker.com/install/linux/docker-ce/ubuntu/).
    
    ```sh
    sudo apt-get update
    
    sudo apt-get --no-install-recommends install -y \
      apt-transport-https \
      ca-certificates \
      curl \
      gnupg-agent \
      software-properties-common
      
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo add-apt-repository \
      "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
      $(lsb_release -cs) \
      stable"
      
    sudo apt-get update
    
    sudo apt-get --no-install-recommends install -y docker-ce docker-ce-cli containerd.io
    
    
    ```
    
-   Perform  [post-installation steps](https://docs.docker.com/install/linux/linux-postinstall/)  to run docker without root permissions.
    
    ```sh
    sudo groupadd docker
    
    sudo usermod -aG docker $USER
    ```


-   Install docker-compose (1.19.0 or newer). Compose is a tool for defining and running multi-container docker applications.
    
    ```bash
    sudo apt-get --no-install-recommends install -y python3-pip python3-setuptools
    
    sudo python3 -m pip install setuptools docker-compose
    ```
    
-   Clone  _CVAT_  source code from the  [GitHub repository](https://github.com/opencv/cvat).
    
    ```bash
    sudo apt-get --no-install-recommends install -y git
    
    git clone https://github.com/opencv/cvat
    
    cd cvat
    
    ```
    
-   Run docker containers. It will take some time to download the latest CVAT release and other required images like postgres, redis, etc. from DockerHub and create containers.
    
    ```sh
    docker-compose up -d
    ```
- You can register a user but by default it will not have rights even to view list of tasks. Thus you should create a superuser. A superuser can use an admin panel to assign correct groups to the user. Please use the command below:

	```sh
	docker exec -it cvat bash -ic 'python3 ~/manage.py createsuperuser'
	```
