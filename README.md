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
