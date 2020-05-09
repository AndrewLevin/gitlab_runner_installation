# gitlab_runner_installation


1) ssh root@amlevin23
2) yum install emacs
3) curl -sSL https://get.docker.com/ | sh
4) mkdir cmspkuewk-container
5) cd cmspkuewk-container
6) wget https://raw.githubusercontent.com/clelange/cmssw-docker/master/cc7-cms/Dockerfile
7) docker build .
8) docker tag XXXXXXXXX cmspkuewk-image
9) docker run -d --name gitlab-runner --restart always -v /srv/gitlab-runner/config:/etc/gitlab-runner -v /var/run/docker.sock:/var/run/docker.sock -v /afs:/afs -v /cvmfs:/cvmfs gitlab/gitlab-runner:latest
10) docker exec -it gitlab-runner gitlab-runner register
11) emacs -nw /srv/gitlab-runner/config/config.toml 

