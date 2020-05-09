# gitlab_runner_installation

1) Go to https://openstack.cern.ch/project/instances/.
2) Launch a CC7 x86_64 m4.large machine.
3) ssh to the machine from lxplus (e.g. [amlevin@lxplus085 ~]$ ssh amlevin@amlevin8)
4) yum -y install emacs wget
5) curl -sSL https://get.docker.com/ | sh
6) service docker start
7) mkdir cmspkuewk-container
8) cd cmspkuewk-container
9) wget https://raw.githubusercontent.com/clelange/cmssw-docker/master/cc7-cms/Dockerfile
10) emacs Dockerfile
11) remove the line starting with "RUN     groupadd -g 1000" and all lines below it
12) docker build .
13) docker tag {hexidecimal number reported at the end of step 10} cmspkuewk-image
14) docker run -d --name gitlab-runner --restart always -v /srv/gitlab-runner/config:/etc/gitlab-runner -v /var/run/docker.sock:/var/run/docker.sock -v /afs:/afs -v /cvmfs:/cvmfs gitlab/gitlab-runner:latest
15) docker exec -it gitlab-runner gitlab-runner register
16) emacs -nw /srv/gitlab-runner/config/config.toml 

