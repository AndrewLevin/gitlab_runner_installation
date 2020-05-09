# gitlab_runner_installation

```
[amlevin@lxplus742 ~]$ ssh root@amlevin23
[root@amlevin23 ~]# yum install emacs
[root@amlevin23 ~]# curl -sSL https://get.docker.com/ | sh
[root@amlevin23 ~]# mkdir cmspkuewk-container
[root@amlevin23 ~]# cd cmspkuewk-container
[root@amlevin23 ~]# wget https://raw.githubusercontent.com/clelange/cmssw-docker/master/cc7-cms/Dockerfile
[root@amlevin23 ~]# docker build .
[root@amlevin23 ~]# docker tag XXXXXXXXX cmspkuewk-image
[root@amlevin23 ~]# docker run -d --name gitlab-runner --restart always -v /srv/gitlab-runner/config:/etc/gitlab-runner -v /var/run/docker.sock:/var/run/docker.sock -v /afs:/afs -v /cvmfs:/cvmfs gitlab/gitlab-runner:latest
[root@amlevin23 ~]# docker exec -it gitlab-runner gitlab-runner register
[root@amlevin23 ~]# emacs -nw /srv/gitlab-runner/config/config.toml 
```
