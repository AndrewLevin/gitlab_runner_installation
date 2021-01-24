# gitlab_runner_installation

1) Go to https://openstack.cern.ch/project/instances/.
2) Launch a CC7 x86_64 m2.large machine.
3) ssh as root to the machine from lxplus(e.g. [root@lxplus085 ~]$ ssh amlevin@amlevin8)
4) yum -y install emacs wget
5) locmap --enable cvmfs
6) locmap --configure cvmfs
7) emacs -nw crontab.txt
8) add the line ** * * * * ls /cvmfs/cms.cern.ch/cmsset_default.sh >& /dev/null
9) crontab crontab.txt
10) curl -sSL https://get.docker.com/ | sh 
11) service docker start
12) mkdir cmspkuewk-container
13) cd cmspkuewk-container
14) wget https://raw.githubusercontent.com/clelange/cmssw-docker/master/cc7-cms/Dockerfile
15) emacs -nw Dockerfile
16) remove the line starting with "RUN     groupadd -g 1000" and all lines below it
17) docker build .
18) docker tag {hexidecimal number reported at the end of the previous step} cmspkuewk-image
19) docker run -d --name gitlab-runner --restart always -v /srv/gitlab-runner/config:/etc/gitlab-runner -v /var/run/docker.sock:/var/run/docker.sock -v /afs:/afs -v /cvmfs:/cvmfs gitlab/gitlab-runner:latest
20) docker exec -it gitlab-runner gitlab-runner register
21) emacs -nw /srv/gitlab-runner/config/config.toml 
22) add the line under [runners.docker]: pull_policy = "if-not-present"
23) change volumes = ["/cache"] to volumes = ["/cache","/afs:/afs","/cvmfs:/cvmfs"]

References:

https://docs.gitlab.com/runner/install/docker.html

https://awesome-workshop.github.io/gitlab-cms/

https://gist.github.com/sashabaranov/defccee8795619025d83f466b0ec4e35

https://docs.docker.com/
