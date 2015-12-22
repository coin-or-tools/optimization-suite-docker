This should be the most easy way to get a setup of the SYMPHONY library for solving mixed-integer-programs.

## install prerequisites
```
# get docker
sudo apt-get install docker.io
# get plain ubuntu image
sudo docker pull ubuntu
```

## install Symphony
```
# get this repository
git clone https://github.com/PatWie/symphony-docker.git
# go into the new directory
cd symphony-docker
# create a docker-image from the provided Dockerfile (tagged as "symphony")
sudo docker build -t symphony image/
```

Now, you can run the library. Currently, this Dockerfile just provides the default interactive shell by typing
```
sudo docker run -it symphony
```
Inside the docker file the Symphony-interpreter can be run by:

```
/var/symphony/bin/symphony
```




