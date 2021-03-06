## Compiling ATS2 from packaged C-source.

Please see the [directions][1] on the ATS site. 

## Compiling ATS2 from github-hosted source.

Please note that compiling ATS2 in this style is recommended
primarily for people who are interested in helping develop ATS2.

ATS2 is implemented in ATS1.
Currently, the required version of ATS1 (ATS/Anairiats) for bootstrapping ATS2 (ATS/Postiats) is 0.2.11.
Assume that you have already installed ATS1-0.2.11.

Checkout Postiats from [sources][2] by downloading the zip file or using the following command (assuming that `~/postiats` is a directory where the repository is to be put locally):


    git clone https://github.com/githwxi/ATS-Postiats.git ~/postiats

Set PATH to include the directory ~/postiats/bin so that the second half of the building process knows where to locate the created "patsopt".

Now, build ATS2:

```
make -f Makefile_devl all
```
This command effectively executes both of the following:

```
make -f codegen/Makefile_atslib # this is only needed for the first time
make -f Makefile_devl
```

Optionally, put `~/postiats/bin` on your PATH, e.g., by adding the following line to your `.bashrc`:

    export PATH=${PATH}:${HOME}/postiats/bin

Finally, a couple of environmental variables need to be properly set:

    export PATSHOME=${HOME}/postiats #For the example install above, or wherever ATS2 is located.

If you also want to use ats2-lang-contrib, then please set the environmental variable PATSHOMERELOC to
the name of the directory where ats2-lang-contrib resides.

## What to try if the build of ATS/Postiats fails

Should the build fail at some point, it may be necessary to clean up:

    make -C src cleanall

If that does not work, it is worth trying to clean up ATSLIB as well:

    make -f codegen/Makefile_atslib cleanall

The above make rule should be executed whenever one wishes to use updated [ATSLIB] code from the upstream github repository.


***

When trying to build ATS2, it is possible that the version of GMP used for the build of ATS1 is no longer the same as that being used for the current build procedure. In that case, do the following, then repeat the build cleanup and make procedures outlined above:

```
cd ${ATSHOME}
atslib libc/SATS/gmp.sats
atslib libc/DATS/gmp.dats

```

Other GMP problems can arise; if you don't care about GMP support in ATS (i.e. you aren't too worried about constraints involving large numbers), then you can bypass GMP support by calling make as follows:

```
make -f Makefile_devl all C3NSTRINTKND=intknd
```

which effectively replaces `gmpknd` with `intknd`. You shoud NOT do this for producing safety-critical production code, but should be find for most development. Also note that if you want to specify linker and library flags for GMP, you must currently do so through the environment variable `LIBGMP`, **not** `LDFLAGS`.

## ATS and Mac OS X

Using ATS under Mac OS X  has been a thorny issue for quite sometime.
Probably the easiest way to install ATS2 under OSX is by using a [homebrew formula](https://github.com/Homebrew/homebrew/blob/master/Library/Formula/ats2-postiats.rb).

Here are some caveats:

1. ATS1 cannot be correctly compiled by clang. You need genuine gcc (the one
on OSX is hooked to clang by default) to compile ATS1. See below.

2. When using gcc-4.x to compile ATS1, please make sure that you generate
a no-gc version of ATS1. Let us refer to this version as ATS1-ngc.

3. Please use ATS1-ngc to compile ATS2.

Sounds complicated? All the steps can be found in [.travis.yml](../../tree/master/.travis.yml).

## Install ATS using package system

### Debian GNU/Linux unstable(sid)

```
$ sudo apt-get install ats2-lang
```

## ATS in a virtual machine

ATS can be installed in a docker container using the following command:

```
docker run -ti -v [your source directory]:/src steinwaywhw/ats 
```

This gives you the ability to edit/compile any ATS code on any platform as long as docker is installed.
More information and the docker install file is available at https://github.com/steinwaywhw/docker-ats. 

A Vagrantfile could be written based on that Dockerfile, which enables booting up a real virtual machine (instead of a container).

[1]: http://www.ats-lang.org/DOWNLOAD
[2]: https://github.com/githwxi/ATS-Postiats