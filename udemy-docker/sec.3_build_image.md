### Image Layers 

$ docker image history <image>
$ docker image inspect 

### Tag and Push and Pull

$ docker login --> stores a session ID 
$ docker logout --> from untrusted host 

$ docker image tag <image> <name/image>

$ docker push <name/image:tag>

$ docker pull nginx:mainline 



### Dockerfile

$ docker build -f <some-Dockerfile>

$ docker build -t <tag> <. directory>

- keep files that change the most at the bottom of the file
- keep files that change the least at the bottom of the file




6 # Overview of this assignment
7 # use the instructions from developer below to create a working Dockerfile
8 # feel free to add command inline below or use a new file, up to you (but must be named Dockerfile)
9 # once Dockerfile builds correctly, start container locally to make sure it works on http://localhost
10 # then ensure image is named properly for your Docker Hub account with a new repo name
11 # push to Docker Hub, then go to https://hub.docker.com and verify
12 # then remove local image from cache
13 # then start a new container from your Hub image, and watch how it auto downloads and runs
14 # test again that it works at http://localhost
