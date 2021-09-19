# ML Trainingcenter

This repository is the training center for the competence **Grundlagen Machine
Learning (gml)** at the Bachelor study program in Data Science at FHNW.


## Setting up the Trainingcenter

Docker is a platform for developing and running applications and it's very
useful for developing Data Science codes in homogeneous environments as well.
We will use JupyterLab inside a Docker Container to be able to run code in a
standard python machine learning environment.

After setting this up you'll be able to connect to JupyterLab inside your
docker container on your local machine through your browser.


### 1. Install Docker on your computer

Depending on your operating system you have to install docker in different ways.  

You'll find detailed instructions here: https://docs.docker.com/get-docker


### 2. Pull the trainingcenter docker image

Authenticate to the GitLab Docker registry with a personal access token, see
details
[here](https://docs.gitlab.com/ee/user/packages/container_registry/#authenticating-to-the-gitlab-container-registry).

Choose scope `read_registry` und `write_registry` to generate the access token.  

```
# login to the FHNW GitLab docker registry first
$ docker login cr.gitlab.fhnw.ch -u <username> -p <token>

# now pull the image
$ docker pull cr.gitlab.fhnw.ch/ml/courses/gml/gml_trainingcenter:v20210220 
```

### 3. Fork this repository

Fork this repository to your own user space by pressing the fork button on the upper right.


### 4. Clone your fork to your computer. 

For this you might wanna set up a ssh-key for your computer, see here: https://docs.gitlab.com/ee/ssh/

In your fork on GitLab find the address with which you can clone your Repo on the upper right. Clone into your gml directory (`MY_GML_DIR`) using:

```
$ git clone MY_REPO_FORK
```


### 5. Create a directory `data` in `MY_GML_DIR`

Here you will place all data files needed for the exercises and mini-challenges.


### 6. Start a trainingcenter container on your machine

```
$ docker run -d \
    -p 8877:8888 \
    --user root \
    -v PATH_TO_MY_GML_DIR:/home/jovyan/work/ \
    -v PATH_TO_MY_GML_DIR/data:/data \
    --name=gml_trainingcenter \
    cr.gitlab.fhnw.ch/ml/courses/gml/gml_trainingcenter:v20210220 \
    start.sh jupyter lab --LabApp.token=''

```

(Replace `PATH_TO_MY_GML_DIR` with the actual path on your computer.)


### 7. Check that your container is running

```
$ docker ps -a
```

### 8. Connect to your container through your browser

Enter `http://localhost:8877/lab` in your browser.


### 9. Restart

If you later on need to restart your container you can just run

```
$ docker start gml_trainingcenter
```


### 10. Fetching new assignments 

Should there be any new assignments released, you can fetch them from the
master repo as follows:

```
# add original repo as remote upstream 
$ git remote add upstream git@gitlab.fhnw.ch:ml/courses/gml/gml_trainingcenter.git

# now whenever you want to merge the changes from the remote upstream repo, ie
the one you forked from, you can do:
$ git pull upstream master
```

.. and add some merge message.

