# gitlab_runner_installation

1) Go to https://openstack.cern.ch/project/instances/.
2) Launch a CC7 x86_64 m2.large machine.
3) ssh to the machine from lxplus (e.g. [amlevin@lxplus085 ~]$ ssh amlevin@amlevin8)
4) yum -y install emacs wget
5) locmap --enable cvmfs
6) locmap --configure cvmfs
7) curl -sSL https://get.docker.com/ | sh 
8) service docker start
9) mkdir cmspkuewk-container
10) cd cmspkuewk-container
11) wget https://raw.githubusercontent.com/clelange/cmssw-docker/master/cc7-cms/Dockerfile
12) emacs -nw Dockerfile
13) remove the line starting with "RUN     groupadd -g 1000" and all lines below it
14) docker build .
15) docker tag {hexidecimal number reported at the end of the previous step} cmspkuewk-image
16) docker run -d --name gitlab-runner --restart always -v /srv/gitlab-runner/config:/etc/gitlab-runner -v /var/run/docker.sock:/var/run/docker.sock -v /afs:/afs -v /cvmfs:/cvmfs gitlab/gitlab-runner:latest
17) docker exec -it gitlab-runner gitlab-runner register
18) emacs -nw /srv/gitlab-runner/config/config.toml 
19) add the line under [runners.docker]: pull_policy = "if-not-present"
20) change volumes = ["/cache"] to volumes = ["/cache",'/afs:/afs','/cvmfs:/cvmfs']

References:

https://docs.gitlab.com/runner/install/docker.html

https://awesome-workshop.github.io/gitlab-cms/

https://gist.github.com/sashabaranov/defccee8795619025d83f466b0ec4e35
