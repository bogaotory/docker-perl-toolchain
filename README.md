[![Build Status](https://travis-ci.org/bogaotory/docker-perl-toolchain.svg?branch=master)](https://travis-ci.org/bogaotory/docker-perl-toolchain)

# Building a Docker image with the Perl toolchain
Build a docker image which includes the *plenv + cpanm + carton* Perl toolchain.
 - [plenv](https://github.com/tokuhirom/plenv) - Perl installation manager
 - [cpanm](https://github.com/miyagawa/cpanminus) - CPAN installer
 - [carton](https://metacpan.org/pod/Carton) - Module dependency manager (like Bundler in Ruby)

### Build the image yourself
Choose your Perl version by changing `PLENV_VERSION` in `Dockerfile` or overwrite `PLENV_VERSION` with the `-e` option
```
cd docker-perl-toolchain
docker build -t [repositoryname] .
```

### Docker image (Automated Build)
The docker image itself is available on Docker Hub:
[docker-perl-toolchain image](https://hub.docker.com/r/bogaotory/docker-perl-toolchain/).

### Example Usage
Suppose you wish to run a script (`corecheck.pl`) which prints the CPU information of the host. Then you would have these three files:

1. `cpanfile`:
 ```
 requires "Sys::Info", "0.78";
 ```

2. `corecheck.pl`:
 ```perl
 use Sys::Info;
 use Sys::Info::Constants qw( :device_cpu );
 my $info = Sys::Info->new;
 my $cpu  = $info->device( CPU => %options );
 
 printf "CPU: %s\n", scalar($cpu->identify)  || 'N/A';
 printf "CPU speed is %s MHz\n", $cpu->speed || 'N/A';
 printf "There are %d CPUs\n"  , $cpu->count || 1;
 printf "CPU load: %s\n"       , $cpu->load  || 0;
 ```

3. `Dockerfile`:
 ```
 FROM bogaotory/perl-toolchain
 
 ADD cpanfile /build/cpanfile
 ADD corecheck.pl /build/corecheck.pl
 
 WORKDIR build
 
 RUN . /etc/profile \
  && carton install # This happens in the WORKDIR, modules are installed in /build/local directory
 
 ENTRYPOINT . /etc/profile \
  && carton exec perl corecheck.pl
 ```

### References
Here is a list of articles/posts/repos I read in order to make this Dockerfile:
 - [Dockerising a Perl application](https://robn.io/docker-perl/)
 - [Modern Perl toolchain for Git managed web apps](http://kappataumu.com/articles/modern-perl-toolchain-for-web-apps.html)
 - [https://github.com/miyagawa/docker-plenv-vanilla](https://github.com/miyagawa/docker-plenv-vanilla)
 - [https://github.com/moltar/docker.plenv](https://github.com/moltar/docker.plenv)
 - [Understanding a little more about /etc/profile and /etc/bashrc](http://bencane.com/2013/09/16/understanding-a-little-more-about-etcprofile-and-etcbashrc/)
 - [Best practices for writing Dockerfiles](https://docs.docker.com/engine/articles/dockerfile_best-practices/)
 - [Which cpan installer is the right one? (CPAN.pm/CPANPLUS/cpanminus)](http://stackoverflow.com/questions/5861292/which-cpan-installer-is-the-right-one-cpan-pm-cpanplus-cpanminus)
 - [Number of CPU/Cores in Perl](http://stackoverflow.com/questions/18360374/number-of-cpu-cores-in-perl)
