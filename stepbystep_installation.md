
[//]: # "**********************************************************"
[//]: # "** INSTALL file for Faiss (Fair AI Similarity Search    **"
[//]: # "**********************************************************"


Docker instructions when you are not using GPU and want to use Jupyter notebook inside the faiss docker
=======================================================================================================

Make sure that docker is installed on your machine
(https://docs.docker.com/engine/installation/) and nvidia-docker
(https://github.com/NVIDIA/nvidia-docker) are installed on your system

To build the "faiss" image, run

  `docker build -t faiss .`

or if you don't want/need to clone the sources, just run

  `docker build -t faiss github.com/facebookresearch/faiss`

Once you have the docker installed, you inside the docker using:-

`docker run -p 8888:8888 -ti --name faiss faiss bash`

In the above command
- the first 8888 is the local port that you want to map and the second 8888 is the docker port

With the above command once you are inside the docker, you need to accomplish the following:-

1. Upgrade you pip

pip install -U pip

2. Install Jupyter 

pip install jupyter

3. Install the basic packages such as sklearn, pandas, numpy, seaborn etc.

pip install sklearn pandas numpy seaborn

4. Check if your jupyter is working by using

jupyter notebook --ip 0.0.0.0 --allow-root

5. Stop jupyter using CTRL+C

6. Create a folder say work inside your docker. You will map this docker folder to some external folder where you have the data which you want to use

mkdir work 
 
Copy the path of this folder using. Keep this handy. We will need this in step 11

pwd

7. Come out your docker using

CTRL P Q

8. Find the docker id using

docker ps - a

9. Save the new docker image to a new image 

docker commit <WHATEVER IS YOUR docker id> faiss_new 

here faiss_new is the name of your new docker image

10. To completely detach from the old docker

docker rm -f <dockerid>

11. Start the new docker image using the following:-  I am assuming all your data is in documents and you need access to that inside the docker

docker run -p 8888:8888 -v /Users/arkidmitra/Documents/:/opt/faiss/work -ti --name faiss_new faiss_new bash

Here /Users/arkidmitra/Documents/ is the local folder you need mapped on a folder inside the docker

/opt/faiss/work is the path of the folder you had created inside the docker

12. Copy the following files to the work directory inside which you will be starting notebook

faiss.py
swigfaiss.py  
_swigfaiss.so 

13. Go inside the work directory

14. RUN your notebook
jupyter notebook

14. Inside the notebook write

import faiss


Thats it!









