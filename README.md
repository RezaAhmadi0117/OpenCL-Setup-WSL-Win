

# OpenCL in WSL(Ubnutu) & Windows(Visual Studio)

## About

Learning how to set up and use the OpenCL library on Windows 

<br/>

---

## Getting Started (WSL Ubnutu)

The easiest way to use and compile accelerated codes using the OpenCL library is to install one of the Linux distributions using Windows Subsystem for Linux (WSL). You can use the following link for installation:

+ [Install Linux on Windows with WSL](https://learn.microsoft.com/en-us/windows/wsl/install)


> Note that to install Windows Subsystem for Linux (WSL), you need Windows 10 version 2004 and higher (Build 19041 and higher) or Windows 11.

After installation, use the following commands to update the available packages and install the required tools.

```console
$ sudo apt update
$ sudo apt upgrade 
$ sudo apt install build-essential
$ sudo apt install ocl-icd-opencl-dev
$ sudo apt install clinfo
```


Then download and install the files needed to install the required drivers based on the processor from the link below. This link shows how to download and install the files.

+ [Install OpenCL Drivers On Ubuntu](https://support.zivid.com/en/latest/getting-started/software-installation/gpu/install-opencl-drivers-ubuntu.html)

> (not recommended) If there was a problem installing the files, You can also access the OpenCL library by installing cuda on WSL. The installation method is available in [this link](https://ubuntu.com/tutorials/enabling-gpu-acceleration-on-ubuntu-on-wsl2-with-the-nvidia-cuda-platform#1-overview).


If you have installed the drivers and tools correctly, by running the **clinfo** command, the output will be displayed as below. Note that the output placed in this document is based on Intel processor information.


```console
Number of platforms                                 1
    Platform Name                                   Intel(R) OpenCL HD Graphics
    Platform Vendor                                 Intel(R) Corporation
    Platform Version                                OpenCL 3.0
    Platform Profile                                FULL_PROFILE
    Platform Extensions                             cl_khr_byte_addressable_store ......    
    Platform Host timer resolution                  1ns
    Platform Extensions function suffix             INTEL

    Platform Name                                   Intel(R) OpenCL HD Graphics
    Number of devices                               1
    Device Name                                     Intel(R) Graphics [0x4c8b]
    Device Vendor                                   Intel(R) Corporation
    Device Vendor ID                                0x8086
    Device Version                                  OpenCL 3.0 NEO
    Driver Version                                  22.39.24347
    Device OpenCL C Version                         OpenCL C 1.2
    Device Type                                     GPU
    Device Profile                                  FULL_PROFILE
    Device Available                                Yes
    Compiler Available                              Yes
    Linker Available                                Yes
    Max compute units                               24
    Max clock frequency                             1300MHz
    Device Partition                                (core)
    Max number of sub-devices                       0
    Supported partition types                       None
    Supported affinity domains                      (n/a)
    Max work item dimensions                        3
    Max work item sizes                             256x256x256
    Max work group size                             256
    Preferred work group size multiple              64
    Max sub-groups per work group                   32
    Sub-group sizes (Intel)                         8, 16, 32

    ...
    ...
    ...
```


Up to this section, the requirements for using the OpenCL library are described. Now, for testing, I use the example in [@ReneHollander](https://github.com/ReneHollander/opencl-example). You can use the following commands to download the files and run the program.

```console
$ git clone https://github.com/ReneHollander/opencl-example.git
$ cd helloworld/
$ g++ -o HelloWorld HelloWorld.cpp -lOpenCL
$ ./HelloWorld
```

<br/>

---

## Getting Started (Visual Studio)

According to the information stated in [this link](https://stackoverflow.com/questions/56858213/how-to-create-nvidia-opencl-project), the OpenCL library is available in Nvidia graphics card drivers, if your system has any of the cards of this company, you can use the ready project in [@ProjectPhysX](https://github.com/ProjectPhysX/OpenCL-Wrapper). 


You should note that in order to run this project, you need to install Visual Studio along with the Desktop development with C++ package. the way to install them is shown in the link below.

+ [Install C and C++ support in Visual Studio](https://learn.microsoft.com/en-us/cpp/build/vscpp-step-0-installation?view=msvc-170)

So install and set up using the command below, get the required files and run the project in the visual studio program.


```console
$ git clone https://github.com/ProjectPhysX/OpenCL-Wrapper
```



An example of the program execution output is shown in the block below. It should be noted that in this project, an external wapper is used to use the library, but you can directly access the Opencl library.



```console
|----------------.------------------------------------------------------------|
| Device ID    0 | NVIDIA GeForce RTX 3070                                    |
| Device ID    1 | Intel(R) UHD Graphics 730                                  |
|----------------'------------------------------------------------------------|
|----------------.------------------------------------------------------------|
| Device ID      | 0                                                          |
| Device Name    | NVIDIA GeForce RTX 3070                                    |
| Device Vendor  | NVIDIA Corporation                                         |
| Device Driver  | 527.56                                                     |
| OpenCL Version | OpenCL C 1.2                                               |
| Compute Units  | 46 at 1800 MHz (5888 cores, 21.197 TFLOPs/s)               |
| Memory, Cache  | 8191 MB, 1288 KB global / 48 KB local                      |
| Buffer Limits  | 2047 MB global, 64 KB constant                             |
|----------------'------------------------------------------------------------|
| Info: OpenCL C code successfully compiled.                                  |
| Info: Value before kernel execution: C[0] = 1.00000000                      |
| Info: Value after kernel execution: C[0] = 5.00000000                       |
...
...
```






