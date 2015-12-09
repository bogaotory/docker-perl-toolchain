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
