# docker-perl-toolchain
Build a docker image which includes the *plenv + cpanm + carton* Perl toolchain.
 - [plenv](https://github.com/tokuhirom/plenv) - Perl installation manager
 - [cpanm](https://github.com/miyagawa/cpanminus) - CPAN installer
 - [carton](https://metacpan.org/pod/Carton) - Module dependency manager (like Bundler in Ruby)

### Usage
Choose your Perl version by changing `PLENV_VERSION` in `Dockerfile` or overwrite `PLENV_VERSION` with the `-e` option
```
cd docker-perl-toolchain
docker build -t [repositoryname] .
```

### Docker image
The docker image itself is available on Docker Hub:
[docker-perl-toolchain image](https://hub.docker.com/r/bogaotory/docker-perl-toolchain/).

### References
Here is a list of articles/posts/repos I read in order to make this Dockerfile:
 - [Dockerising a Perl application](https://robn.io/docker-perl/)
 - [Modern Perl toolchain for Git managed web apps](http://kappataumu.com/articles/modern-perl-toolchain-for-web-apps.html)
 - [https://github.com/miyagawa/docker-plenv-vanilla](https://github.com/miyagawa/docker-plenv-vanilla)
 - [https://github.com/moltar/docker.plenv](https://github.com/moltar/docker.plenv)
 - [Understanding a little more about /etc/profile and /etc/bashrc](http://bencane.com/2013/09/16/understanding-a-little-more-about-etcprofile-and-etcbashrc/)
 - [Best practices for writing Dockerfiles](https://docs.docker.com/engine/articles/dockerfile_best-practices/)
 - [Which cpan installer is the right one? (CPAN.pm/CPANPLUS/cpanminus)](http://stackoverflow.com/questions/5861292/which-cpan-installer-is-the-right-one-cpan-pm-cpanplus-cpanminus)
