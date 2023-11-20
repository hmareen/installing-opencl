# Getting OpenCL to work

This document is geared toward getting OpenCL to work for CG-lab4. If you cannot get it to compile, build and run properly, even when following the instructions below, **leave an issue** [here](https://github.com/jlartois/installing-opencl/issues) **or send us an email**.

## NVidia
For those with an NVidia GPU, installing the CUDA Toolkit (and rebooting) seems to suffice to get OpenCL to work.

## Apple
For those with an Apple computer, OpenCL seems to work out of the box.

## AMD
1. Windows: OpenCL seems to be supported through the Adrenalin driver. _Has anyone tried this?_
2. Ubuntu 20.04 or 22.04: installing the ROCm packages seems to suffice. _Has anyone tried this?_

## Intel
### Windows
_Has anyone tried this? I will be testing this out ASAP and update the readme._

According to [this webpage](https://www.intel.com/content/www/us/en/developer/articles/tool/opencl-drivers.html#proc-graph-section), when scrolling down to "Windows* OS":
> Intel® Graphics Compute Runtime for OpenCL™ Driver is included with the Intel® Graphics Driver package for Windows* OS.
> ...
> The graphics driver package is built in with Windows* 10 OS install.

So it seems that OpenCL should work? Otherwise you could try to download the latest "Intel® Graphics Driver" from the suggested "Intel® Download Center" or "Intel® Driver Update Utility".

### Ubuntu 22.04, also WSL with Ubuntu 22.04
_I tested this on a fresh Ubuntu and WSL, and it works for me._
```
sudo apt update -y
sudo apt full-upgrade -y
sudo apt install clinfo
clinfo                         # returns 0 platforms
sudo apt install ocl-icd-opencl-dev -y
sudo apt install opencl-headers

# to test if libOpenCL.so is properly installed:
sudo apt install apt-file -y   # to find files
sudo apt-file update           # necessary
apt-file find libOpenCL.so     # returns 4 results, including:
                               # ocl-icd-libopencl1: /usr/lib/x86_64-linux-gnu/libOpenCL.so.1
                               # ocl-icd-opencl-dev: /usr/lib/x86_64-linux-gnu/libOpenCL.so
                               # so that's good

clinfo                         # still returns 0 platforms
```

Since clinfo is still not detecting OpenCL, we need to install the Intel runtimes as follows. Go to [this webpage](https://www.intel.com/content/www/us/en/developer/articles/tool/opencl-drivers.html#proc-graph-section) and scroll down to "Linux* OS". Check if gcc is installed:

```
sudo apt install gcc g++ -y   # install gcc, g++ if this was not already the case
gcc --version                 # returns 11.4, which is >=7.3
```
We checked earlier if libOpenCL.so was installed. So lastly click [Manual Download and install](https://github.com/intel/compute-runtime/releases) and scroll down to "Installation procedure on Ubuntu 22.04". Follow the instructions:
```
mkdir neo
cd neo
wget ...                      # wget the 7 .deb files
sudo dpkg -i *.deb
```
That's it, normally clinfo should work now:
```
clinfo                        # now works and returns 1 platform: Intel(R), OpenCL 3.0
```
Compiling, building and runing CG-lab4 should also work.

## Other Linux distros
Check out the first paragraph in the [FAQ](https://github.com/intel/compute-runtime/blob/master/FAQ.md) of the Intel runtimes repository. It elaborates on the supported OS's.

_I have not tested this. Did the instructions above work for you, or not?_
