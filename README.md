# Antlr4's Jenkin Build - Benchmarks, Code Coverage etc.

Have a look at http://jenkins.wx.io:8080/.
It'll probably be up till the end of the month (March 2017).

![Google Compute Engine 2Core Hicpu](https://github.com/wxio/antlr4-jenkins/raw/master/benchmark-build-cge-2core-highcpu.png)

![Local Docker Benchmarking](https://github.com/wxio/antlr4-jenkins/raw/master/benchmark-builds.png)

```
git clone https://github.com/wxio/antlr4-jenkins.git
docker build -t antlr4-jenkins .
docker run -p 8080:8080 -p 50000:50000 -v `pwd`/jenkins_home:/var/jenkins_home antlr4-jenkins
```
When running goto
http://localhost:8080/job/antlr4-benchmark/build?delay=0sec


* Benchmark local code
Run a local git server and change you build parameters accordingly.
This assumes all your code is under one directory.
With Go code this would look like
```
myproject
  src
    github.com/mycode
	github.com/antlr/antlr4
```

From the src directory run the following git command.
```
git daemon --reuseaddr --base-path=. --export-all --verbose --enable=receive-pack
```

## Install Jekins on Ubuntu manually

```
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
```
Then add the following entry in your 
```
/etc/apt/sources.list:
```

```
deb https://pkg.jenkins.io/debian-stable binary/
```
Update your local package index, then finally install Jenkins:

```
sudo apt-get update
sudo apt-get install jenkins
```

## Reading material
This was based on this

http://www.asciiarmor.com/post/99010893761/jenkins-now-with-more-gopher

https://github.com/ryancox/go-jenkins-setup/blob/master/Dockerfile


Uses modified plot plugin for Pipeline

https://github.com/MarkusDNC/plot-plugin


Go get this along the way

https://github.com/wxio/gobench2plot

modified from

https://gist.github.com/wavded/5e6b0d5016c2a3c05237

Based on Official Jenkins Docker

https://hub.docker.com/_/jenkins/


## TODO
add code coverage

https://github.com/t-yuki/gocover-cobertura

https://github.com/envimate/golang-coverage-report

https://github.com/axw/gocov/

https://github.com/t-yuki/gocov-xml

https://github.com/jstemmer/go-junit-report

https://github.com/envimate/golang-coverage-report

https://github.com/t-yuki/gocover-cobertura

intergate with existing antlr tests

https://github.com/antlr/antlr4/blob/master/doc/antlr-project-testing.md

move to CGE or some other host

https://docs.docker.com/machine/drivers/gce/

https://kubernetes.io/docs/user-guide/volumes/


https://mrooding.me/dockerized-jenkins-2-on-google-cloud-platform-34747725e786#.ejsk1n4nh

https://jpetazzo.github.io/2015/09/03/do-not-use-docker-in-docker-for-ci/