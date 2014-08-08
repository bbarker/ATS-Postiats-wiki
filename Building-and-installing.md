## Compiling ATS/Postiats from source archives

Please see the [directions][1] on the ATS site. 

## Compiling ATS/Postiats from git sources (developer version).


Assuming you've got ATS/Anairiats functioning on your system, you can use it to bootstrap Postiats (currently version 0.2.11 is required). Please proceed as described next.

Checkout Postiats from [sources][2] by downloading the zip file or using the following command (assuming that `~/postiats` is a directory where the repository is to be put locally):


    git clone https://github.com/githwxi/ATS-Postiats.git ~/postiats

Set PATH to include the directory ~/postiats/bin so that the second half of the building process knows where to locate the created "patsopt".

Now, build ATS2:

```
make -f Makefile_devl all
```
This command effectively run both of the following:

```
make -f codegen/Makefile_atslib # this is only needed for the first time
make -f Makefile_devl
```

Optionally, put `~/postiats/bin` on your PATH, e.g., by adding the following line to your `.bashrc`:

    export PATH=$PATH:$HOME/postiats/bin

Finally, a couple of environmental variables really need to be set. 

    export PATSHOME=$HOME/postiats #For the example install above, or wherever ATS2 is located.
    export PATSHOMERELOC=$PATSHOME #For the git install only these are equal to each other.

In general, ${PATSHOMERELOC} is the directory where you put ats2-lang-contrib.
The current plan is to use PATSHOMERELOC for supporting automatically downloading ATS packages located on the Internet.

## What to try if the build of ATS/Postiats fails

Should the build fail at some point, it may be necessary to clean up:

    make -C src cleanall

If that does not work, it is worth trying to clean up atslib as well:

    make -f codegen/Makefile_atslib cleanall

The above make rule should be executed whenever one wishes to use updated [atslib] code from the upstream github repository.

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