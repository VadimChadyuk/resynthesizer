The file vagga.yaml is a vagga script for testing the build process of resynthesizer.
It builds resynthesizer in a disposable container (a VM.)
Vagga builds as a user, without requiring root privileges.
You can modify the script to easily test building on many versions of Linux and GIMP,
without affecting your machine.

Vagga is a tool to create development environments in containers.
To use this script, you first need to install vagga.
See https://vagga.readthedocs.io/en/latest/what_is_vagga.html.
Vagga uses Linux; using vagga on Windows and OSX is inside a Docker VM.

Then:
    >mkdir <foo>
    copy this script to the directory
    >cd <foo>
    >vagga   (will list commands offered by this script.  Expect e.g. "gimpversion...listResynth...")
    >vagga listResynth (tells vagga to run the command "listResynth")

The first time you do this, it will take a long time, building containers by downloading many packages and compiling.
At the end, expect a list of resynthesizer components as installed in the container.

Subsequently, you can modify the script and again >vagga listResynth.
Whenever the script is modified, vagga will check whether to rebuild containers and may seem to hang, so be patient.

You can and should then delete the containers.
The containers are stored completely in the large, hidden directory .vagga in the current directory, owned by you.
Just delete that directory.

I used this script to test building on 
Ubuntu 18.10 (cosmic) with the GIMP 2.10.6 packaged for that distribution,
and on Ubuntu 19.04 (disco) with GIMP 2.10.8, 
while my machine was still on 16.04 and GIMP 2.8.
To test building resynthesizer on the next version of Ubuntu,
I will simply need to change one word in the script: disco => eoan.
I think that you could similarly test that resynthesizer will build on many recent Linux distributions
(by changing the baseOS container.)

The script will also test that the package gimp-plugin-registry installs resynthesizer.
(That package is usually built by Debian and Ubuntu.)

The script will also test that the make install scripts install resynthesizer properly:
so that it is invokeable from GIMP (not that it has the intended image effect.)

The script is readable and documents (again) the basic requirements to build resynthesizer
(which have not changed recently.)
The scripts illustrate the rats nest of dependencies, including required tools and libraries.
For example, you can build resynthesizer without installing GIMP or Python,
but resynthesizer won't install or run, i.e. GIMP and Python are runtime dependencies.


